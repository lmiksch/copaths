# Cocopaths - A Compiler for contranscriptional folding pathways

[![codecov](https://codecov.io/gh/lmiksch/cocopaths/graph/badge.svg?token=6PVQSOEK8R)](https://codecov.io/gh/lmiksch/cocopaths)
## Getting Started
To install the package you need to clone the repository using git: 

```bash
# Clone this repository
$ git clone https://github.com/lmiksch/cocopaths

#Change your directory 
$ cd copaths
```

The package can then be installed via pip:

```bash
$ pip install .
```

For development purpose:

```bash
$ pip install -e .
```

Afterwards use pytest to verify that all tests are working:
```bash
$ pytest
```

After installation you can try if the script is installed by using:
```bash
$ cocopaths --help
```

The script gets called by using:
```bash
$ cocopaths 
```

the abstract folding path(AFP) can be either put in as a .txt file or directly in the terminal

The AFP must have following propperties to be translated to a domain level sequence:
  - Pseudoknot-Free
  - If a structure was defined it can't be changed if no additional step influences the defined substructure

# How to use cocopaths and cocosim 


Cocopaths and cocosim can be used in a pipeline to simulate the resulting domain level sequence

```bash
$ cocopaths -i test.txt | cocosim 
```

In the examples directory, you can find sample inputs for both cocopaths and cocosim.

A typical command might look like this:

```bash
$ cocopaths -i fp_1.txt | cocosim 
```

Using only the command without input will prompt you to enter the domain-level sequence in the terminal.

```bash
$ cocosim 
```

```bash
$ cocosim 
Please enter a domain level sequence:
```


### Current Bugs: 
 - CocoPaths
  - Following Path is not possible but still accepted: 
    - Desired: ['.', '()', '().', '(..)', '(...)', '(.(.))']
    - Simulat: ['.', '()', '.()', '(())', '(().)', '(()..)']
    - see prob1.txt 
 
 
 - Cocosim:
  - Complementary domains must be separated by another domain 
  - sometime segmentation fault(coredumped) during steps -> bug not reproducable
  - if spacer length = 0 following error: 
    
  peppercornenumerator/peppercornenumerator/condense.py", line 200, in condense
    const = (self.get_condensed_rate(prxn), '/M' * (len(reactants)-1) + '/s')
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  peppercornenumerator/peppercornenumerator/condense.py", line 234, in get_condensed_rate
    assert 0 <= reactant_probabilities < 1.000001
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  AssertionError



### CocoPathsToDO: 

  - investigate floating point errors/ number error i think they are floating point errors 
    - add rounding to 10-15 comma stellen
  
    - enforce_cutoff_macrostate
      - dont know if setting occupancy to 0 is enough or if should remove cut complex from macrostate
      - current implemenation keeps the complex in the macrostates
      
  - write analysis script to make some statistics about whats possible to design and what not 

  - begin with design of nucleotide sequences


  - peppercornenumerator.enumerator.PolymerizationError: Too many reactions enumerated! (50049)
