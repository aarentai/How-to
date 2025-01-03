## [Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html)
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
### `yield`
Analogous to `return`, but won't stop at the first `yield`
```
yield a           
yield from [a, b, c]
``` 

## list
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

## [torch](https://pytorch.org/docs/stable/)
### [Monitering memory usage](https://pytorch.org/docs/stable/generated/torch.cuda.memory_summary.html)
```
torch.cuda.memory_summary(device=f'cuda:0')
```

### [Checkpoint the model to save memory](https://pytorch.org/docs/stable/checkpoint.html)
```
modules = [module for k, module in self._modules.items()][0]
output = torch.utils.checkpoint.checkpoint_sequential(modules, len(modules), x)
```

### [Model parallel](https://pytorch.org/tutorials/intermediate/model_parallel_tutorial.html)
```
class ToyModel(nn.Module):
    def __init__(self):
        super(ToyModel, self).__init__()
        self.net1 = torch.nn.Linear(10, 10).to('cuda:0')
        self.relu = torch.nn.ReLU()
        self.net2 = torch.nn.Linear(10, 5).to('cuda:1')

    def forward(self, x):
        x = self.relu(self.net1(x.to('cuda:0')))
        return self.net2(x.to('cuda:1'))
```

### [Pipeline parallel](https://pytorch.org/docs/stable/pipeline.html?highlight=data+parallel)
```
# Need to initialize RPC framework first.
os.environ['MASTER_ADDR'] = 'localhost'
os.environ['MASTER_PORT'] = '29500'
torch.distributed.rpc.init_rpc('worker', rank=0, world_size=1)
# Build pipe.
fc1 = nn.Linear(16, 8).cuda(0)
fc2 = nn.Linear(8, 4).cuda(1)
model = nn.Sequential(fc1, fc2)
model = Pipe(model, chunks=8)
input = torch.rand(16, 16).cuda(0)
output_rref = model(input)
```

### [Data parallel](https://pytorch.org/docs/stable/generated/torch.nn.DataParallel.html?highlight=model+parallel)
```
net = torch.nn.DataParallel(model, device_ids=[0, 1, 2])
output = net(input_var)  # input_var can be on any device, including CPU
```

### [Distributed data parallel](https://pytorch.org/docs/stable/notes/ddp.html?highlight=ddp)
```
import torch
import torch.distributed as dist
import torch.multiprocessing as mp
import torch.nn as nn
import torch.optim as optim
from torch.nn.parallel import DistributedDataParallel as DDP


def example(rank, world_size):
    # create default process group
    dist.init_process_group("gloo", rank=rank, world_size=world_size)
    # create local model
    model = nn.Linear(10, 10).to(rank)
    # construct DDP model
    ddp_model = DDP(model, device_ids=[rank])
    # define loss function and optimizer
    loss_fn = nn.MSELoss()
    optimizer = optim.SGD(ddp_model.parameters(), lr=0.001)

    # forward pass
    outputs = ddp_model(torch.randn(20, 10).to(rank))
    labels = torch.randn(20, 10).to(rank)
    # backward pass
    loss_fn(outputs, labels).backward()
    # update parameters
    optimizer.step()

def main():
    world_size = 2
    mp.spawn(example,
        args=(world_size,),
        nprocs=world_size,
        join=True)

if __name__=="__main__":
    # Environment variables which need to be
    # set when using c10d's default "env"
    # initialization mode.
    os.environ["MASTER_ADDR"] = "localhost"
    os.environ["MASTER_PORT"] = "29500"
    main()
```

### [Automatic mixed precision package](https://pytorch.org/docs/stable/amp.html)
```
# Creates model and optimizer in default precision
model = Net().cuda()
optimizer = optim.SGD(model.parameters(), ...)

for input, target in data:
    optimizer.zero_grad()

    # Enables autocasting for the forward pass (model + loss)
    with autocast():
        output = model(input)
        loss = loss_fn(output, target)

    # Exits the context manager before backward()
    loss.backward()
    optimizer.step()
```

## [logging](https://docs.python.org/3/library/logging.html)
```
logging.info("\n%s", report)
```

## [tqdm](https://tqdm.github.io/)
```
from tqdm import tqdm
for i in tqdm(range(1000)):
  pass
```

## file handle
### write
| Parameter |  Mode  |                            Operations                            |
|:---------:|:------:|:----------------------------------------------------------------:|
| 'w'       | write  | will overwrite any existing content, and create it if not exists |
| 'a'       | append | will append to the end of the file, and create it if not exists  |
| 'x'       | create | create a file, returns an error if the file exist                |
```
with open(path, 'w') as f:
  f.write()
```

### read
```
with open(path, 'r') as f:
  f.read()
  f.readline()
```

## [subprocess](https://docs.python.org/3/library/subprocess.html)
The subprocess module allows you to spawn new processes, connect to their input/output/error pipes, and obtain their return codes.

```
import subprocess
subprocess.run(["pip3","install","--user","pydicom"])   # -- for word
subprocess.run(["pip3","install","-u","pydicom"])       # - for letter
```

## [glob](https://docs.python.org/3/library/glob.html)
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

## [argparse](https://docs.python.org/3/library/argparse.html)
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

## [os](https://docs.python.org/3/library/os.html)
|         Command         |                   Function                  | Counterpart in shell |
|:-----------------------:|:-------------------------------------------:|:--------------------:|
|      `os.getcwd()`      |        Get current working directory        |         `pwd`        |
| `os.mkdir("path/to")` |              Create a directory             |        `mkdir`       |
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



## [absl.flag](https://abseil.io/docs/python/guides/flags)
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

## [itkwidgets](https://pypi.org/project/itkwidgets/0.12.1/)
Interactive Jupyter widgets to visualize images, point sets, meshes and their combinations on the web.

If `view()` cannot show anything, use the following command to solve:
```
jupyter nbextension install --py itkwidgets --user
jupyter nbextension enable --py itkwidgets
```

- `view()`: displays the 2D or 3D scalar field images or point sets.
```
import itk
from itkwidgets import view

image = itk.imread(file_name)
view(image)                                                                       # 2D image
view(image, rotate=True, axes=True, vmin=4000, vmax=17000, gradient_opacity=0.9)  # 3D image

import numpy as np
number_of_points = 3000
gaussian_1_mean = [0.0, 0.0, 0.0]
gaussian_1_cov = [[1.0, 0.0, 0.0], [0.0, 2.0, 0.0], [0.0, 0.0, 0.5]]
point_set_1 = np.random.multivariate_normal(gaussian_1_mean, gaussian_1_cov, number_of_points)
view(point_sets=[point_set_1])                                                    # 3D point set
view(image=image, point_sets=[point_set_1])                                       # 3D point set laying over image

from pyvista import examples
airplane = examples.load_airplane()
view(geometries=airplane)                                                         # 3D mesh
view(image=image, geometries=airplane)                                            # 3D mesh laying over image
```

- `checkerboard()`: overlays one image over another, and visualizes them simultaneously in form of checkerboard. Applicable to both 2D or 3D images.
```
import itk
from itkwidgets import checkboard

image1 = itk.imread(file_name1)
image2 = itk.imread(file_name2)
checkerboard(image1, image2, pattern=5)
```

- `compare()`: compares the two images side by side.
```
import itk
from itkwidgets import compare

image1 = itk.imread(file_name1)
image2 = itk.imread(file_name2)
compare(image1, image2, link_cmap=True)
```

- `line_profile()`: plots intensity along the line begining with point1 and end with point2.
```
import itk
from itkwidgets import line_profile

image = itk.imread(file_name)
line_profile(image, point1=[35.3, 169.7, 113.6], point2=[325.1, 197.3, 204.6], ui_collapsed=True)
```

## [pyvista](https://docs.pyvista.org/index.html)
`pyvista` is mainly used as a mesh generator, and the generated object can be used as the `geometries` argument in `itkwidgets.view`
```
import pyvista as pv
mesh = pv.read('my_strange_vtk_file.vtk')                       # read .vtk file
```

```
import pyvista as pv
spline = pv.Spline(points, 1000)                                # create a plain line object with 1000 interpolation points(numpy array[num, dim])
tube = spline.tube(radius=0.1)                                  # covert the line object to a tube object

ellipsoid = pv.ParametircEllipsoid((xradius=None, yradius=None, zradius=None, center=None, direction=None))

from itkwidgets import view
view(image, geometries = [tube, ellipsoid])
```

## [itk](https://itkpythonpackage.readthedocs.io/en/master/Quick_start_guide.html#usage)

## [skimage](https://scikit-image.org/docs/stable/api/api.html)