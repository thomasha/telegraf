# dirstat Input Plugin

The dirstat plugin gathers metrics about file existence, size, and other stats. 
This is mostly the filestat plugin that has been changed.


### Configuration:

```toml
# Read stats about given directory
[[inputs.dirstat]]
  ## Files to gather stats about.
  ## These accept standard unix glob matching rules, but with the addition of
  ## ** as a "super asterisk". See https://github.com/gobwas/glob.
  files = ["/etc/telegraf/telegraf.conf", "/var/log/**.log"]
  ## If true, read the entire file and calculate an md5 checksum.
  md5 = false
```

### Measurements & Fields:

- dirstat
    - filecount
    - oldestfile

### Tags:

- All measurements have the following tags:
    - file (the path the to file, as specified in the config)

### Example Output:

```
$ telegraf --config /etc/telegraf/telegraf.conf --input-filter dirstat --test
* Plugin: filestat, Collection 1
> dirstat,file=/tmp/foo/bar,host=tyrion filecount=0i,oldestfile=0i 1528188065000000000
```
