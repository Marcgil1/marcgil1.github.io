---
title: "Mathematics End-of-Degree Thesis"
date: 2023-05-22
draft: false
showTableOfContents: true
showReadingTime: false
---

{{< katex >}}

{{< button href="/pdf/tfg-mat-doc.pdf" target="_self" >}}
View thesis PDF
{{< /button >}}

Please, find the LaTeX source files for the thesis in the following
[link](https://github.com/Marcgil1/tfg-mat-doc). You may also find the
associated code [here](https://github.com/Marcgil1/tfg-mat-code). Even though
this article is being writen and published in late 2023, the thesis was
presented in June 2023, all code and source files dating from that time.

## Introduction

This article introduces the end-of-degree thesis I completed in fulfillment of
the requeriments for obtaining the bachelor's degree in Mathematics at the
University of Murcia. This work was supervised by Prof. Dr. Alfredo Marín, from
the same institution.

The thesis verses on the _Rank Pricing Problem_ (henceforth, RPP) a
combinatorial optimisation problem consisting in determining the best possible
way to price a given set of items in such a manner that the total profit for the
retailer is maximised, while taking into account the preferences and budgets of
a set of customers.

Results presented in this thesis are adaptable to a number of use cases, most of
them relating to supporting business leadership in pricing different models of a
same type of product. Thus, using terminology currently in vogue, its main
application case would be that of business intelligence; in particular,
decission support. Practical ussage would require developing several generic
user profiles by aggregating already existing customer behaviour data.

## Formal definition of the problem

The RPP presupposes the existence of a seller and of a set of clients. The
seller offers various goods and wishes to prize them so as to maximise his
benefits. In turn, each client is characterised by a list of preferences. These
lists consist of products from those offered by the seller.  Products in them
are totally ordered, so that for each pair of distinct products \\(i_1\\) and
\\(i_2\\) in the preference list of some customer \\(k\\), either \\(i_1\\) is
strictly better than \\(i_2\\) for \\(k\\), or \\(i_2\\) is strictly better than
\\(i_1\\) for \\(k\\).  Furthermore, each client has a budget, which is the
maximum amount of money he can afford to expend. In this setting, the RPP is
defined as the problem of determining for each client wishes one product of
maximum preference for him whose price be less than or equal to his budget. From
this assignment we may then trivially recover the seller's profit.

## Project scope and individual contributions

In line with the standard procedure for master's thesis in the University of
Murcia, the work carried out during this project mainly consisted in
synthetising an academic paper. In this case, the paper was due to Calvete et
al. [2019], where the RPP was first introduced and studied.

Other than reviewing the aforementioned paper, this thesis includes some
individual contributions. In particular, the base study carried out by Calvete
was expanded in order to deal with the _Envy-free, Capacitated Rank Pricing
Problem_, in which we allow to define a limited ammount of products, in contrast
to the standard Rank Pricing Probelm, which presupposes an unlimited supply of
all items.

A second individual contribution consisted in developing a code implementation
of this problems by using the mathematical programming language AMPL.
Furthermore, some computational studies were carried out on this novel version
of the problem. In order to easy reproducibility, these studies were carried out
programmatically through Python scripts made available alongside the AMPL code
[[here](https://github.com/Marcgil1/tfg-mat-code)].

## Document overview

The thesis is structured in five chapters:
1. An introduction to the fields of linear, integer, and bilevel programming,
   which are used for modelling the RPP. Furthermore, some concepts of Graph
   Theory are introduced which are necessary for giving theoretical evidence on
   the quality of the formulations presented later on.
2. Some naive formulations of the RPP are introduced which follow the Bilevel
   Programming paradigm. They are used for deriving some other integer non-linear
   formulations which are more computationally tractable. This is a schema followed
   at several points in the thesis: deriving more computationally-tractable
   formulations from harder-to-solve ones.
3. Chapter three continues improving the non-linear integer formulations
   obtained by the end of the last chapter by linearising them through
   inclussion of a novel set of variables. In fact, two natural ways of
   linearising the problem exist, each leading to a different linear formulation
   with its own set of variables. Both are presented and form the basis of the
   rest of the thesis.  Furthermore, two algorithms are introduced for variable
   separation. These are used for speeding up the computational resolution of
   the previously-obtained formulations. This approach falls within the
   _brach-and-cut_ approach to solving integer programming problems.
4. Chapter four is a miutious study of a particular subproblem of the RPP: the
   Set Packing Subproblem. This is a well-known problem in Integer Programming,
   and some ingenious results due to Padberg [1973] are used for giving
   theoretical results giving a concrete picture of how _tight_ restrictions in
   the presented formulations are. This is a theoretically-sound way of saying
   that the given formulations can be solved within a reasonable amount of time.
5. Finally Chapter five concentrates all individual contributions. These include
   extending the previous work, which is due to Calvete et al. [2019], to an
   extension of the RPP which allows modelling the situation in which a seller
   wishes to sell some items which have stock limitations. For this matter,
   extensions of the formulations due to Calvete are developed. Furthermore, some
   computational studies are carried out assessing how the solving time for these
   formulations scales with the problem size.

## Code overview

Source files for this project are grossly divided into two main classes: first,
AMPL files defining the several models considered; second, Python scripts
automating the various aspects of the computational study which the model files
will be subject to.

Scripts follow a convention I developed some time ago automating the different
stages of a project. This simply consists of having a directory `mk` under which
to store several scripts automating repetitive actions. This is a bit more
flexible than having makefiles, since we get all the expressive power of our
interpreter of choice, be that Python, a shell, or any other. Indeed, this is an
idea which is quite far from being revolutionary, but I've found that its
simplicity makes it preferable to more complex tools like Gradle or Maven
whenever these may be avoided.

Anyway, the project implements two main scripts: `mk/gendata` and `mk/run`. The
first one randomly generates entry data in the format expected by AMPL and
stores it in the `data` folder. The second script iterates over this folder and
automates execution of the solver, as well as generation of graphs and LaTeX
tables.

### Code dependencies.

The code depends for execution on:
1. The Rich Python library [[pip link](https://pypi.org/project/rich/)].
2. The Amplpy Pyhton library [[pip link](https://pypi.org/project/amplpy/)].
3. Having a correct installation of AMPL in the executing machine.

## Bibliography

- Calvete, H. I., Domínguez, C., Galé, C., Labbé, M., and
  Marín, A. (2019). The rank pricing problem: Models and branch-and-cut
  algorithms. _Computers & Operations Research_, 105:12–31.
- Padberg, M. W. (1973). On the facial structure of set packing polyhedra.
  _Mathematical Programming_, 5:199–215.
