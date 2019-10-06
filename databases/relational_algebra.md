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
      * Also known as Cartesian product
      * Returns a combination of attributes inside 2 relations.
      * E.g. Consider 2 relation: R (A, B, C) & S (X, Y).
        * R × S returns a relation with schema (A, B, C, X, Y)
    * Union (∪)
      * Returns a relation containing all tuples that occur in R and/or S.
      * E.g. Find all customer and restaurant names.
        * π<sub>rname</sub>(Sells) ∪ π<sub>cname</sub>(Customers)
    * Intersect (∩)
      * Returns a relation containing all tuples that occur in R and S.
      * E.g. Find all pizzas that contain both cheese and chilli.
        * π<sub>pizza</sub>(σ<sub>ingredient = 'cheese'</sub>(Contains)) ∩ π<sub>pizza</sub>(σ<sub>ingredient = 'chilli'</sub>(Contains))
    * Difference (−)
      * Returns a relation containing all tuples that occur in R but not in S.
      * E.g. Find all pizzas that contain both cheese and chilli.
        * π<sub>pizza</sub>(σ<sub>ingredient = 'cheese'</sub>(Contains)) - π<sub>pizza</sub>(σ<sub>ingredient = 'chilli'</sub>(Contains))
* Join algebra operators
  * Natural Join (⋈)
    * Acts similar to SQL Natural Join.
    * Join 2 relations with a common attributes.
    * E.g. Find all restaurant that sells to some customers in some areas.
      π<sub>rname, area</sub>(Restaurants) ⋈ π<sub>cname, area</sub>(Customers)
  * Theta Join (⋈<sub>condition</sub>)
    * Acts similar to SQL Inner Join
    * Join 2 relations with any number of specific condition
    * E.g. Find all restaurant that sells to some customers in the same area.
      π<sub>rname, area</sub>(Restaurants) ⋈ <sub>Restaurants.area = Customers.area</sub> π<sub>cname, area</sub>(Customers)
  * Division (÷)
    * This is not implemented in SQL
    * Returns tuples with all combinations in S that are present in R.
    * E.g. Find restaurants that sells all kinds of pizza.
      π<sub>rname, pizza</sub>(Sells) ÷ π<sub>pizza</sub>(Pizzas)
  