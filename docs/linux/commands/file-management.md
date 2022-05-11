# File Management
This document consists of frequently used commands to work with files in Linux

## File size
### Calculate file(s) size with du
`-b`:   show file size instead of disk usage  
`-c`:   show total file(s) size at the end  
`-h`:   show human readable format  

```bash
# Calculate each directory's size inside current working directory
du -bch

# Calculate multiple files size
du -bch [filename/pattern]
```
