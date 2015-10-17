Navigation
==========

This is the source code of two simple navigation experiments: an obstacle avoidance and a maze navigation. Neural networks are generated thanks to the sferes framework to solve these tasks. Several different fitness functions are provided for comparison as well as process helpers like behavioral diversity or novelty.

These experiments have illustrated tutorials given by Stephane Doncieux on selective pressures. This was part of a larger tutorial covering different topics in evolutionary robotics and given by Nicolas Bredeche, Jean-Baptiste Mouret and Stephane Doncieux at:
* Artificial Life conference, New York, 2014
* GECCO, Madrid, 2015
* ECAL, York 2015


Usage & installation
--------------------

### Dependencies:
sferes2 core (https://github.com/sferes2/sferes2)
sferes2 modules:
* fastsim (https://github.com/jbmouret/libfastsim for the core library and https://github.com/sferes2/fastsim to connect it to sferes)
* nn2 (https://github.com/sferes2/nn2)

sferes2 has its own dependencies (notably boost, tbb and eigen). Check sferes2 documentation for more details.

### Installation

In the following, it is assumed that all the git repositories have been cloned in ~/git.

First, libfastsim need to be compiled:
    cd ~/git/libfastsim
    ./waf configure
    ./waf build

Before compiling the experiment, the following instructions need to be executed:
    cd ~/git/sferes2/modules
    ln -s ~/git/fastsim
    ln -s ~/git/nn2
    cd ~/git/sferes2/exp
    ln -s ~/git/navigation
    cd ~/git/sferes2/
    echo fastsim >> modules.conf
    echo nn2 >> modules.conf

To compile the experiment:
    ./waf configure
    ./waf build --exp=navigation

### Launching an experiment and viewing the results

To run an experiment, launch one of the executables in ~/git/sferes2/build/default/exp/navigation. It will create a directory with the generated results.
gen_XX files contain the best individual(s) of the generation XX. To look at its behavior, launch the following command:
    my_executable -o data --load=gen_XX
where my_executable is the the program that has generated gen_XX and XX the generation number to look at.

### Experiments in sferes

An experiment describes what is to be evolved, how and how it is evaluated. The experiments provided here contain mostly the evaluation part (the fitness function). The other parts are standard sferes2 modules.

Variants of an experiments are defined using macros. This is the reason why the source conde contains many
    #ifdef VARIANT1
       // what to do for VARIANT1
    #else
       // what to do for other variants 
    #endif

A variant of an experiment is defined by a set of labels. The choice of the variants to compile is made in the wscript file. The variant with the labels VARIANT1 FIT1 ENV1 of an exp my_exp.cpp creates an executable called my_exp_variant1_fit1_env1.

### Obstacle avoidance

Simple experiment in which a two wheeled robot has to avoid obstacles. Several fitness functions have been defined: FIT1, FIT2 and FIT3 to illustrate the impact of their definition on the results (don't expect much fom FIT1...). Likewise, three different environment of increasing difficulty have been defined: ENVOA1, ENVOA2 and ENVOA3.

### Maze navigation

Experiment in which the robot has to find how to go out of a maze. The variants are the fitness: FITDIST telle to take into account the distance to the output, otherwise it is a binary fitness function (success or failure). The DIVERSITY variant includes a behavioral diversity process helper and the NOVELTY variant includes a novelty search objective. Without any of them, it does not work at all, with the DIVERSITY, some experiment do converge, with NOVELTY, most of them do.

Author
-------
- Stephane Doncieux stephane.doncieux@isir.upmc.fr: main author and maintainer

Other contributors
------------
- Jean-Baptiste Mouret


See sferes2 main documentation for an overview of this framework. 



