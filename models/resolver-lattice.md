---
id: resolver-lattice-001
title: "Resolver Lattice"
status: "asserted"
class: "resolution-model"
version: "0.1"
depends_on:
  - "monad-nature-001"
reasserting_resolver: "Chad Coulter"
---

# Resolver Lattice

## Assertion Provenance

This model is reasserted by Chad Coulter and is used as a dependency within this repository.

## Universal Lattice

The universal lattice contains all potential resolver relationships.

## Relative Lattice

For a given Monad, the relative lattice is the resolver space expressed for that Monad.

Each relationship in the relative lattice has a dynamic strength.

Let:

`L_U` = universal lattice

`L_i` = relative lattice for Monad `M_i`

`w_ij` = dynamic strength of the resolver relationship from `M_j` within the resolution space of `M_i`

Then:

`L_i = {(M_j, w_ij)}`

## Core Distinction

`Universal lattice != relative lattice`

The universal lattice expresses potential connectivity.

The relative lattice expresses dynamically weighted resolver strength within a particular Monad's resolution space.
