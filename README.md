# SEESAW: Scalable Error Analysis of Conditional Floating Point Programs

Seesaw similar to its predecessor [Satire](https://github.com/arnabd88/Satire) is a first order error analysis tool for 
obtaining rigorous bounds on worst case floating point round-off errors. But unlike Satire, Seesaw works on 
floating-point programs WITH conditions. Seesaw, attains scalability, bound tightness and provides analysis on control 
flow divergence through a combination of incremental analysis, abstraction, SMT solving, and judicious use of concrete 
and symbolic evaluation.

# Quick Start

Minimal commands to create a Python environment, install dependencies, and run Seesaw:

```bash
python3 -m venv .venv
. .venv/bin/activate
pip install sly symengine sympy bigfloat numpy
export PATH=/path/to/gelpia/bin:$PATH
python3 src/satire+.py --help
python3 src/satire+.py --std --file tests/smartRoot.txt
```

If `gelpia` is not already installed, build it first by following the Gelpia README, then make sure
its `bin` directory is available on `PATH`.

# Dependencies

Satire requires the following softwares to be installed.

* Requirements:
	* python > 3.6
	* python packages using pip3
		* [sly](https://github.com/dabeaz/sly) > 0.3
		* [symengine](https://github.com/symengine/symengine) > 0.5.1
		* [sympy](https://www.sympy.org/en/index.html) > 1.4
		* [bigfloat](https://pypi.org/project/bigfloat) > 0.4.0
		* [numpy](https://numpy.org/)
	* [gelpia](https://github.com/soarlab/gelpia) (branch: constraints. working commit ID: 2ee03ee7a59f117f0fe92d41e5ad6492203d27f6)
		* After installation, make `gelpia/bin` available in `$PATH`
	* Optional:
		* RealPaver support via `RL1/build/libsatrp.so` for `--realpaver`

## Setup

Seesaw is a Python-based framework. The main entrypoint is `src/satire+.py`.

For normal runs, Seesaw now auto-detects the repository root and only requires:

* `python3`
* the Python packages listed above
* `gelpia` available on `$PATH`

If you want to use `--realpaver`, then `RL1/build/libsatrp.so` must exist. In that case,
you can optionally set:

```bash
export SAT_ROOT=/path/to/Seesaw
```

If `SAT_ROOT` is not set, Seesaw falls back to the repo root automatically.

## Usage

The main function is available in `src/satire+.py`.
The "--help" command clarifies all the supporting arguments. Some of the functionality such as abstraction and parallel 
is the same as Satire and has been demonstrated in Satire repository. Currently, Seesaw does not have empirical analysis
support like Satire but it will be added soon. Here we will explain the additional functionality that is not present in 
Satire.

Basic smoke test:

```bash
export PATH=/path/to/gelpia/bin:$PATH
python3 src/satire+.py --help
```

#### Example1 (with constraints)
  > python3 src/satire+.py --std --file tests/smartRoot.txt

[TODO]

#### Example2 (with stats)
  > python3 src/satire+.py --std --file Benchmarks/test2/SAT/test2.txt --stat

[RECHECK. Probably wrong. Remove if not necessary] Prints out error statistics everytime discontinuities are merged.

#### Example3 (with instabilities)
  > python3 src/satire+.py --std --file Benchmarks/test2/SAT/test2.txt --report-instability

Prints out the sorted instability list.
