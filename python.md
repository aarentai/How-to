# [Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html)
### `try`, `except`, `else`, `finally`
The try statement works as follows.
- First, the `try` clause (the statement(s) between the `try` and `except` keywords) is executed.
- If no exception occurs, then goes to `else`
- If an exception occurs, then goes to `except`. If its type matches the exception named after the `except` keyword, the `except` clause is executed, and then execution continues after the try statement.
- Whether exception occurs or not, it will finally goes to `finally`.
```
try:
  x = int(input("Please enter a number: "))
  break
except ValueError as error:
  pass 
else:
  pass
finally:
  pass
```
### `pass`
In Python programming, the pass statement is a null statement. Nothing happens when the pass is executed.
```
for i in xrange(1000): 
  pass
```
### `raise`
```
def functionName( level ):
    if level < 1:
        raise Exception("Invalid level!", level)
```
### `assert`
When the expression is False, trigger the exceptions.
```
assert expression
```
is equivalent to
```
if not expression:
  raise AssertionError
```

# list
### `extend()` vs `append()`
```
a1 = [1, 2]
a2 = [1, 2]
b = (3, 4)

# a1 = [1, 2, 3, 4]
a1.extend(b) 

# a2 = [1, 2, (3, 4)]
a2.append(b)
```

### `insert()`
```
vowel = ['a', 'e', 'i', 'u']

# 'o' is inserted at index 3
# the position of 'o' will be 4th
vowel.insert(3, 'o')
```

### `any()`
Return `true` if at least one item in iterable is `true`
```
any(iterable)
```

# [logging](https://docs.python.org/3/library/logging.html)
```
logging.info("\n%s", report)
```

# [subprocess](https://docs.python.org/3/library/subprocess.html)
The subprocess module allows you to spawn new processes, connect to their input/output/error pipes, and obtain their return codes.

```
import subprocess
subprocess.run(["pip3","install","--user","pydicom"])   # -- for word
subprocess.run(["pip3","install","-u","pydicom"])       # - for letter
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

# [argparse](https://docs.python.org/3/library/argparse.html)
The `argparse` module makes it easy to write user-friendly command-line interfaces. The program defines what arguments it requires, and argparse will figure out how to parse those out of `sys.argv`.

```
import argparse

parser = argparse.ArgumentParser(description='Process some integers.')
parser.add_argument('--theta', 
                    default   = None, 
                    type      = int, 
                    required  = True,
                    help      = 'value of theta'
                    )
parser.add_argument('--train', 
                    action    = 'store_true'
                    help      = 'whether to train or not'
                    )

args = parser.parse_args()
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

## [matplotlib.pyplot](https://matplotlib.org/stable/api/pyplot_summary.html)
```
from matplotlib import pyplot as plt

fig = plt.figure()
ax  = fig.add_subplot()
ax.plot(x, y, label, color)
```

### interactive plot
```
%matplotlib widget
```

## [numpy](http://numpy.org)
### 

## [pytorch](http://pytorch.org)
### `autograd`
`torch.Tensor` is the central class of the package. If you set its attribute `.requires\_grad` as `True`, it starts to track all operations on it. When you finish your computation you can call `.backward()` and have all the gradients computed automatically. The gradient for this tensor will be accumulated into `.grad` attribute.

To stop a tensor from tracking history, you can call `.detach()` to detach it from the computation history, and to prevent future computation from being tracked.

To prevent tracking history (and using memory), you can also wrap the code block in `with torch.no\_grad():`. This can be particularly helpful when evaluating a model because the model may have trainable parameters with `requires\_grad=True`, but for which we don’t need the gradients.

There’s one more class which is very important for autograd implementation - a `Function`.

`Tensor` and `Function` are interconnected and build up an acyclic graph, that encodes a complete history of computation. Each tensor has a `.grad\_fn` attribute that references a Function that has created the Tensor (except for Tensors created by the user - their `grad\_fn` is `None`).

If you want to compute the derivatives, you can call `.backward()` on a `Tensor`. If Tensor is a scalar (i.e. it holds a one element data), you don’t need to specify any arguments to `backward()`, however if it has more elements, you need to specify a gradient argument that is a tensor of matching shape. 

Typical pipeline:
```
x.requires_grad_()
out = function(x)
out.backward()
gradient = x.grad    
```