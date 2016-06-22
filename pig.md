# Content
- [Tips](#Tips)
- [Data Types](#Data Types)
- [Operators](#Operators)
- [Demo](#Demo)

## Tips
- DUMP or STORE is required to generate output
- Case Sensitivity
  - sensitive: relations, fields, function
  - insensitive: keywords

## Data Types
### relations, bags, tuples, fields
- a relation is a bag(outer bag)
- a bag is a collection of tuples
- a tuple is an oredered set of fields
- a field is a piece of data

获取field:
- positional notation(start with 0): e.g: $0 $1 $2
- name

获取complex data type:
- use dot to access the fields in the tuples

### Data Type
- Simple Types:
  - int
  - long
  - float
  - double
  - chararray
  - bytearray
  - boolean
  - datetime
  - biginteger
  - bigdecimal
- Complex Types:
  - tuple: (field [, field ...])
  - bag:
    - inner bag: {tuple [, tuple ...]}
    - outer bag
  - map: [key#value <, key#value ...>]

## Operators
- Basic:
  - LOAD <data> AS <schema>;
  - FOREACH <relation> GENERATE <field>;
  - FILTER <relation> BY <condition>;
  - FLATTEN
  - DUMP
  - STORE
  - DESCRIBE
- Relation Operators:
  - GROUP/COGROUP:
    - GROUP for one relation
    - COGROUP for two or more relations
  - CROSS: cross product fo two or more relations
  - DISTINCT
  - UNION
  - SPLIT: SPLIT A INTO X IF f1<7, Y IF f2==5, Z IF (f3<6 OR f3>6);
  - LIMIT: LIMIT alias n;

## Common Usage
### Intersection
```
interRaw = JOIN dsp1 BY bidId, dsp2 BY bidId;
```

### Difference
```
co = COGROUP dsp1 BY bidId, dsp2 BY bidId;
dsp1co = FILTER co BY IsEmpty(dsp2);
dsp1only = FOREACH dsp1co GENERATE FLATTEN(dsp1);
dsp2co = FILTER co BY IsEmpty(dsp1);
dsp2only = FOREACH dsp2co GENERATE FLATTEN(dsp2);
```

## Demo
```
SET job.name [adhoc][exchange][2016-06-02-1];
SET job.priority HIGH;

REGISTER 'hdfs:///data/piglib/mvad/*.jar';
REGISTER 'hdfs:///data/piglib/thrift/*.jar';
REGISTER 'hdfs:///data/piglib/common/*.jar';
REGISTER 'hdfs:///data/piglib/elephantbird/*.jar';
/**/
raw = LOAD '$input' using com.mediav.thrift.pig.ThriftB64LineLogLoader('exchange.thrift.LogInfo');

/*
  filter record with no response and no bidInfo, get mvad win records
*/

noNULL = FILTER raw BY response is not NULL and response.bidInfo is not NULL;

-- two types
/*
  one slot to one ad
*/
mvWin = FILTER noNULL BY response.winnerId == 100;

mvFlatBid = FOREACH mvWin GENERATE response.winPrice, FLATTEN(response.bidInfo), request.mobileInfo;

mvBid = FILTER mvFlatBid BY dspId == 100 and adsInfo.bidPrice > 0;

mvUp = FOREACH mvBid GENERATE winPrice-adsInfo.mvPrice as diff, mobileInfo;

/*
  one slot to some ads
*/
filterNULL = FILTER noNULL BY response.bidInfo.adsInfo is not NULL and response.dealInfos is not NULL;

flatDealInfo = FOREACH filterNULL GENERATE FLATTEN(response.dealInfos), response.bidInfo, request.mobileInfo;

mvWinList = FILTER flatDealInfo BY dealInfos::winnerId == 100;

flatBidInfo = FOREACH mvWinList GENERATE FLATTEN(bidInfo), dealInfos::winPrice, dealInfos::creativeId, mobileInfo;

mvBidInfo = FILTER flatBidInfo BY dspId == 100;

mvBidList = FOREACH mvBidInfo GENERATE  FLATTEN(adsInfo.adInfos), dealInfos::winPrice, dealInfos::creativeId, mobileInfo;

linkData = FILTER mvBidList BY adInfos::creativeId == dealInfos::creativeId;

diffPrice = FOREACH linkData GENERATE dealInfos::winPrice-adInfos::mvBasePrice as diff, mobileInfo;

-- total
alldiff = UNION mvUp, diffPrice;

-- mobile VS PC
SPLIT alldiff INTO mobile IF mobileInfo is not NULL, pc IF mobileInfo is NULL;

-- CPM to CPOne: div 10e3; To yuan: div 10e6
smobile = FOREACH (GROUP mobile ALL) GENERATE (double)SUM(mobile.diff)/1000000000.0 as mm, 0.0 as pp;
spc = FOREACH (GROUP pc ALL) GENERATE (double)SUM(pc.diff)/1000000000.0 as pp, 0.0 as mm;
un = UNION smobile, spc;

res = FOREACH (GROUP un ALL) GENERATE SUM(un.mm), SUM(un.pp); 
DUMP res;

```
