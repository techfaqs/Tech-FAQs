# Introduction to Relational Algebra
* A formal language for asking queries on relations.
* A query is composed of a collection of operators called relational operators.
* Each operator takes one/two relations as input and computes an output relation.

* Basic relational algebra operators
  * Unary operators: 
    * Selection (σ)
      * Selects tuples from relation R that satisfy selection condition c.
      * E.g. Find all restaurants, the pizzas that they sell and their prices, where the price is under $20.
        * σ<sub>price < $20</sub>(Sells)
    * Projection (π)
      * Projects attributes given by a list ℓ of attributes from relation R.
      * Duplicated record are removed in output relation.
      * E.g. Find all restaurants and the pizzas that they sell.
        * π<sub>rname, pizza</sub>(Sells)
    * Renaming (ρ)
      * Give a new schema to a relation.
      * E.g. Shops = ρ<sub>Shops(sname)</sub>(π<sub>rname</sub>Sells)
  * Binary operators: 
    * Cross-product (×)
    * Union (∪)
    * Intersect (∩)
    * Difference (−)
