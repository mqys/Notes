c->ctrl m->command
C-->>byte,line(none language)
M-->>word,sentence,paragraph(language)

### MOVE

```
// page down
C-v 
// page up
M-v
// move cursor to center/top/bottom
C-l

// back/froward/previous/next
C-b/f/p/n
// move by word
M-b/f

// move to line start/end
C-a/e
// move to sentence start/end
M-a/e

// move page start/end
M-</>
```

### Manipulation Text

```
// repeat input char
M-number + <char>

// delete char before/after
<del> / C-d

// delete word before/after
M-<del> / M-d

// delete from cursor to line/sentence end
C-k / M-k
 
```

### command

```
// exit
C-x C-c

// repeat commands
C-u + number + <command>
M-number + <command>
// Exception: 
// roll number lines, not pages
C-u number C/M-v

// cancel command
C-g

// leave only one window
C-x 1

```