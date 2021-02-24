# [subprocess](https://docs.python.org/3/library/subprocess.html)
The subprocess module allows you to spawn new processes, connect to their input/output/error pipes, and obtain their return codes.

```
import subprocess
subprocess.run(["pip3","install","--user","pydicom"])
```

# [glob](https://docs.python.org/3/library/glob.html)
Return a list of path names that match pattern.

```
>>> import glob
>>> glob.glob('./[0-9].*')
['./1.gif', './2.txt']
>>> glob.glob('*.gif')
['1.gif', 'card.gif']
>>> glob.glob('?.gif')
['1.gif']
>>> glob.glob('**/*.txt', recursive=True)
['2.txt', 'sub/3.txt']
>>> glob.glob('./**/', recursive=True)
['./', './sub/']
```

# [os](https://docs.python.org/3/library/os.html)
|         Command         |                   Function                  | Counterpart in shell |
|:-----------------------:|:-------------------------------------------:|:--------------------:|
|      `os.getcwd()`      |        Get current working directory        |         `pwd`        |
| `os.makedir("path/to")` |              Create a directory             |        `mkdir`       |
|  `os.chdir("path/to")`  |     Change the current working directory    |         `cd`         |
|  `os.rmdir("path/to")`  |              Remove a directory             |        `rmdir`       |
| `os.listdir("path/to")` | Return a list of all file or directories under the path |         `ls`         |
| `os.scandir("path/to")` | Same as `listdir`, but return a iterator and better performance   |         `ls`         |

|              Command             |                         Function                        |
|:--------------------------------:|:-------------------------------------------------------:|
|    `os.path.isdir("path/to")`    |                  Check if a path exists                 |
|  `os.path.isfile("path/to.txt")` |                  Check if a file exists                 |
|   `os.path.getsize("path/to")`   |           Return the size, in bytes, of path.           |
| `os.path.normpath("path/./to/")` | Normalize a pathname by collapsing redundant separators |
|    `os.path.join("path","to")`   |     Join one or more path components intelligently.     |
|    `os.path.split("path/to")`    |    Split the pathname path into a pair, (head, tail)    |



# [absl.flag](https://abseil.io/docs/python/guides/flags)
```
from absl import app
from absl import flags

FLAGS = flags.FLAGS

# Flag names are globally defined!  So in general, we need to be
# careful to pick names that are unlikely to be used by other libraries.
# If there is a conflict, we'll get an error at import time.
# flags.DEFINE_*('argv_name', default value, discription)
flags.DEFINE_string('name', 'Jane Random', 'Your name.')
flags.DEFINE_integer('age', None, 'Your age in years.', lower_bound=0)
flags.DEFINE_boolean('debug', False, 'Produces debugging output.')
flags.DEFINE_enum('job', 'running', ['running', 'stopped'], 'Job status.')


def main(argv):
  if FLAGS.debug:
    print('non-flag arguments:', argv)
  print('Happy Birthday', FLAGS.name)
  if FLAGS.age is not None:
    print('You are %d years old, and your job is %s' % (FLAGS.age, FLAGS.job))


if __name__ == '__main__':
  app.run(main)
```