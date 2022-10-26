# AlphaStar.

AlphaStar is a package from
[DeepMind](http://deepmind.com) that provides the tools to train an agent to
master StarCraft II offered by [Blizzard Entertainment](http://blizzard.com).

Regarding research efforts, there are two main milestones that can relate with
this open source release. The first one, Paper published at [Nature](https://www.seas.upenn.edu/~cis520/papers/RL_for_starcraft.pdf) 
and presented [ICML 2019 Reinforcement Learning workshop](https://slideslive.com/38917653/alphastar-mastering-the-game-of-starcraft-ii),
presents an **online learning** - learning through interaction with an evironment- 
type of scenario: however, there are concepts not covered in this release,
such as the multi-agent league. For other open-source approaches heavily based on
AlphaStar, please visit [mini-AlphaStar](https://github.com/liuruoze/mini-AlphaStar)

The second research effort, [AlphaStar Unpluggued](https://openreview.net/forum?id=Np8Pumfoty), focus in offline reinforcement
learning -learning through data coming from game replays-. The work benchmarks and present a set of agents , culminating in one thatoverpass the published Nature paper release. This agent is based in a set of agents in the offline setting and offline setting with online learning.
However, this is not part of the open source release.

This release allows you to reproduce all the offline settings and sets the benchmark
for the online setting, so it kicks of an imitation learning scenario. 

As part of our open-sourcing efforts to drive more research interest around
StarCraft II, we provide the following key offerings with this package:

1.  General purpose [architectures](https://github.com/deepmind/alphastar/tree/main/alphastar/architectures)
    to train StarCraftII agents  that can be used with different learning algorithms in
    online and offline settings.

2.  Data readers, offline training and evaluation scripts for fully [offline
    reinforcement learning with Behavior Cloning](https://github.com/deepmind/alphastar/tree/main/alphastar/unplugged)
    as a representative example.

## Setup

We have tested AlphaStar only in **Python3.9** and **Linux**. Currently, we do
not support other operating systems and recommend users to stick to Linux.
The supported StarCraft game version for reproducibility tested in this repository is 
[4.8.2](https://github.com/Blizzard/s2client-proto#downloads)

### Preliminaries

We recommend using a Python virtual environment to manage dependencies. This
should help to avoid version conflicts and just generally make the installation
process easier.

```shell
python3 -m venv alphastar
source alphastar/bin/activate
pip install --upgrade pip setuptools wheel
```

AlphaStar depends on [PySC2](https://github.com/deepmind/pysc2) converters for
data generation and evaluation. Since the code for converters is written in C++,
any changes to the converter code will require recompiling the PySC2 native
extensions. Because of this we offer two different ways to use AlphaStar:

1.  **Installing AlphaStar with `pip`**: this option requires the least setup.
    However if you make changes to PySC2, or if you want to use a version for
    which no pre-built wheel is available, you will need to manually build and
    install a new wheel for PySC2.
2.  **Building AlphaStar using Bazel**: in this case AlphaStar and PySC2 are
    built together from source. By default the PySC2 sources are fetched
    from GitHub. If you wish to use a local repository instead (e.g. because you
    have made local modifications to PySC2) you should modify
    `alphastar/WORKSPACE` as described in the comments.

#### Installing with `pip`

If you're interested in running the bleeding edge versions, you can do so by
cloning our GitHub repository and then executing the following command from the
main directory (where `setup.py` is located):

```
pip install -e .  # For an editable version
pip install .     # For a non-editable version
```

Note that this will also install all the dependencies of AlphaStar.

### Building with Bazel

First, install Bazel by following the instructions
[here](https://docs.bazel.build/versions/main/install-ubuntu.html).

PySC2 requires C++ 17, so Bazel builds of AlphaStar + PySC2 must use
`--cxxopt='-std=c++17'`. For example, to build all AlphaStar targets, run the
following command from the workspace root:

```shell
bazel build --cxxopt='-std=c++17' ...
```

To recursively run all of the tests within the `architectures/` subdirectory:

```shell
bazel test --cxxopt='-std=c++17' architectures/...
```

See the documentation for
[AlphaStar Unplugged](https://github.com/deepmind/alphastar/blob/master/alphastar/unplugged/README.md)
for example `run` commands.

Note: Bazel caches Python package dependencies downloaded from `pip`. To clear
this cache (for example if you have edited `requirements.txt`), run `bazel clean
--expunge`.

You may wish to use a
[.bazelrc file](https://docs.bazel.build/versions/main/guide.html#bazelrc-the-bazel-configuration-file)
to avoid the need to repeatedly specify command-line options, for instance
`--cxxopt='-std=c++17'`.

## Quickstart

For quickstart instructions on how to run training and evaluation scripts in
*fully offline* settings, please refer to
[this README](https://github.com/deepmind/alphastar/blob/master/alphastar/unplugged/README.md). In
this repository, we have not provided any online RL training code. But, the
architectures are fit to be used in both online and offline training.

## About

Disclaimer: This is not an official Google product.

If you use the agents, architectures and offline RL benchmarks published in this
repository, please cite our
[AlphaStar Unplugged](https://openreview.net/pdf?id=Np8Pumfoty) paper.
