---
layout: default
title: Orders
---

Orders
===

Now let's talk about order. Given a set of objects, there can be numerous criteria, based on which to order them, and which depend on the objects themselves - size, weight, age, alphabetical order etc.

![Balls](balls.svg)

However, as mathematicians we are not interested in the *criteria* that we can use to order objects, but in the *nature of the relationship* that defines the order. Of which there can be several types as well. 

Mathematically we can represent order as a *set of things* (e.g. colorful balls) and *a binary relation* between these things (which we often represent as a bunch of arrows). Not all binary relationships are orders - only ones that fit certain criteria that we are going to examine as we review the different types of order.

Linear order
===

The most straightforward type of order that you think about is linear order i.e. one in which every object has its place depending on every other object. In this case the ordering criteria is completely deterministic and leaves no room for ambiguity in terms of which element comes before which. For example, ordering the colors by the length of their waves (or by how they appear in the rainbow).

![Linear order](linear_order.svg)

In most programming languages, we can order objects linearly by providing a function which, given two objects, tells us which one of them is "bigger" (comes first) and which one is "smaller".

```
[1, 3, 2].sort((a, b) => { 
  if (a > b) {
    return true 
  } else {
    return false
  } 
})
```

But in order for such a function to really define an order (e.g. give the same output every time, independent of how the objects were shuffled initially), it has to obey several rules. 

Incidentally, (or rather not incidentally at all), these rules are nearly equivalent to the mathematical laws that define the criteria of the relationship between elements in an order i.e. those are the rules that define which element can point to which. Let's review them.

Reflexivity 
---

Let's get the most boring law out of the way - each object has to be bigger or equal to itself, or **a ≤ a** (the relationship between elements in an order is commonly denoted as **≤** in formulas, but it can also be represented with a simple arrow from first object to the second). 

![Reflexivity](reflexivity.svg)

No special reason for this law to be so, except that the "base case" should be covered somehow. 

We can formulate it the opposite way too and say that each object should *not* have the relationship to itself, in which case we would have a relation than resembles *bigger than*, as opposed to *bigger or equal to* and a slightly different type of order, sometimes called a *strict* order.

Transitivity
---

The second law is maybe the least obvious, (but probably the most essential) - it states that if object **a** is bigger than object **b**, it is automatically bigger than all objects that are smaller than object **b** or **a ≤ b and b ≤ c ➞ a ≤ c**. 

![Transitivity](transitivity.svg)

This is the law that to a large extend defines what an order is: if I am better at playing soccer than my grandmother, then I would also be better at it than my grandmother's friend, whom she beats, otherwise I wouldn't really be better than her.

Antisymmetry
---

The third law is called antisymmetry and it states that the function that defines the order should not give contradictory results (**a ≤ b ⟺ b ≰ a**). 

![antisymmetry](antisymmetry.svg)

It also means that no ties are permitted - either I am better than my grandmother at soccer or she is better at it than me.

Totality
---

The last law is called *totality* (or *connexity*) and it mandates that all elements that belong to the order should be comparable - **a ≤ b or b ≤ a**. That is, for any two elements, one would always be "bigger" than the other. 

By the way, this law makes the reflexivity law redundant, as it is just a special case of reflexivity when **a** and **b** are one and the same object, but I still want to present it for reasons that will become apparent soon.

![connexity](connexity.svg)

You might say that this law is not as self-evident as the rest of them - if you think about different types of real-life objects that we typically order, you would probably think of some situations in which it does not apply. For example, if we aim to order all people based on soccer skills there are many ways in which we can rank a person compared to their friends their friend's friends etc. but there isn't a way to order groups of people who never played with one another.

Orders that resemble the order of people based on their soccer skills in that they don't follow the totality law are called **partial orders** and they are actually much more interesting than linear orders (which are also called **total orders**, by the way). 

**Task:** Think about some orders that you know about and figure out whether they are partial or total.

But before we dive into the world of partial orders, let's say a few things about the numbers.

The order of natural numbers
---

Natural numbers form a linear order under the operation **bigger or equal to** (the symbol of which we have been using in our formulas).

![numbers](numbers.svg)

In many ways, numbers are the quintessential order - every finite order of objects is isomorphic to a subset of the order of numbers, as we can map the first element of any order to the number **1**, the second one to the number **2** etc (and we can do the opposite operation as well).

If we think about it, this isomorphism is actually closer to the everyday notion of order, than the proper definition (the one defined by the laws) - when most people think of order, they aren't thinking of a *transitive, antisymmetric* and *total* relation, but are rather thinking about criteria based on which they can decide which object comes first, which comes second etc.

![Linear order isomorphisms](linear_order_isomorphism.svg)

From the fact that any finite order of objects is isomorphic to the natural numbers it also follows that all linear orders of the same magnitude are isomorphic to one another.

**Question:** If all orders are isomorphic with one another, why do we say that numbers are the quintessential order?

So the linear order is a perfect order, but it is also (and I think that these theorems prove it) the most *boring* order ever, especially when looked from a category-theoretic viewpoint - all finite linear orders are just isomorphic to the natural numbers (by the way, most infinite orders are isomorphic to the natural numbers as well, with the exception of the ones for which Cantor's diagonal argument applies) and so all of their diagrams look the same way.

![Linear order (general)](general_linear_order.svg)

However, this is not the case with partial orders that we will look into next.

Partial order 
===

Like linear orders, a partial orders consists of a set plus a relation, with the only difference that, although it still obeys the *reflexive, transitive* and the *antisymmetric* laws, the relation does not obey the law of *totality*, that is not all of the sets elements are necessarily ordered. I say "necessarily" because even if all elements are ordered, the partial order is still a partial order (just as a group is still a monoid) - all linear orders are also partial orders, but not the other way around (we can even create an *order of orders*, based on which is more general).

If we revisit the example of the soccer players rank list, we can see that the first version that includes just **m**yself, my **g**randmother and her **f**riend is a linear order.

![Linear soccer player order](player_order_linear.svg)

However, including this **o**ther person whom none of us played yet, makes the hierarchy non-linear.

![Soccer player order - leftover element](player_order_leftover.svg)

This is the main difference between partial and total orders - partial orders cannot provide us with a definite answer of the question who is better than who. But sometimes this is what we need - in sports, as well as in other domains, there isn't always an appropriate way to rate people linearly. 

Chains
---

Before, we said that all linear orders can be represented by the same chain-like diagram, we can reverse this statement and say that all diagrams that look something different than the said diagram represent partial orders (or preorders). An example of this is a partial order that contains a bunch of linearly-ordered subsets, e.g. in our soccer example, we can have separate groups of friends who play together and are ranked with each other, but not with anyone from other groups.

![Soccer order - two hierarchies](player_order_two.svg)

The different linear orders that make up the partial order are called *chains*. There are two chains in this diagram **M ➞ G ➞ F** and **D ➞ O**.

The chains in an order don't have to be completely disconnected from each other in order for it to be partial, they can be connected as long as the connections are not all *one-to-one* i.e. when the last element from one chain should not be connected to the first element of the other one (as this would effectively unite them into one chain). But there are other types of connections, like *one-to-many* and *many-to-one*.

![Soccer order - two hierarchies and a join](player_order_two_join.svg)

The above set is not linearly-ordered - although the connection establishes the relationship between **D** and **G** (**D ≤ G**) and although the relationship between **F** and **G** is known as well (**F ≤ G**), the relationship between **D** and **F** is *not* known. Any element can be bigger than the other one.


Maximum and minimum 
---

Although posets don't give us definitive answer to who is better than who, some of them still can give us an answer to the more important question (in sports, as well as in other domains), namely *who is number one*, who is the champion, the player who is better than anyone else, or more generally the element that is bigger than any other element. 

We call such elements the *maximum element* and some (not all) partial orders do have such element - in our last diagram **M** is the maximum element, in this diagram, the green element is the biggest one.

![Join diagram with one more element](join_additional_element.svg)

Sometimes we have more than one elements that are bigger than all other elements, in this case none of them are maximum.

![A diagram with no maximum element](non_maximal_element.svg)

In addition to the maximum element, a partial order may also have a minimum (smallest) element, which is defined in the same way.

Joins
---

The *least upper bound* of two elements that are connected as part of an order is called the *join* of these elements, e.g. the green element is a join of the other two. 

![Join](join.svg)

There can be multiple elements bigger than **A** and **B** (all elements that are bigger than **C** are also bigger than **A** and **B**), but only one of them is a join. Formally, the join of **A** and **B** is defined as the smallest element **C** that is bigger than both **A** and **B** (i.e. for which **A ≤ C**, and **B ≤ C**. 

![Join with other elements](join_other_elements.svg)

Given any two elements in which one is bigger than the other (e.g. **A ≤ B**), the join is the bigger element (in this case **B**). 

In a totally ordered set, the *join* of any subset of elements is just their the *maximum* element. 

Like with the maximum element, if two elements have several upper bounds that are equally big, then none of them is a *join* (a join must be unique).

![A non-join diagram](non_join.svg)

If, however, one of those elements is established as bigger than another, it immediately qualifies.

![A join diagram](non_join_fix.svg)

**Question:** Which concept in category theory reminds you of joins?

Meets
---

Given two elements, the biggest element that is smaller than both of them is called the *meet* of these elements.

![Meet](meet.svg)

The same rules as for the joins apply. 

Interlude: Hasse diagrams
---

In this section, we use what are called "Hasse diagrams" - they are much like our usual diagrams, however they have an additional rule that is followed - "bigger" elements are always positioned above smaller ones. 

In terms of arrows, the rule means that if you add an arrow to a point, the point *to* which the arrow points must always be above the one *from* which it points.

![A join diagram](hasse.svg)

This arrangement allows us to compare any two points by just seeing which one is above the other e.g. to spot the *join* of two elements, you just have to identify the ones they connect to and see which one is lowest.

Examples of partial orders 
===

We all know many examples of total orders (any form of chart or ranking is a total order), but there are probably not so many obvious examples of partial orders that we can think of off the top of our head. So let's see some. In addition to providing a little context, this will help us understand joins and see why are they significant.

Color order
---

To stay true to our form, let's revisit our color-mixing monoid and create a color-mixing partial order in which all colors point to colors that contain them.

![A color mixing poset](color_mixing_poset.svg)

If you go through it, you will notice that the join of any two colors is the color that they make up. Nice, right?

![Join in a color mixing poset](color_mixing_poset_join.svg)

Numbers by division
---

When we order numbers by "bigger or equal to", they form a total order (*the* total order even). But numbers can also form a partial order, for example if we order them by the relationship of which divides which, like if **A** divides **B**, then **A** is before **B** e.g. because **2 * 5 = 10**, **2** and **5** come before **10** (but **3**, for example does not).

![Divides poset](divides_poset.svg)

And it so happens (actually for very good reason) that the join operation again corresponds to an operation that is relevant in the context of the objects - the join of two numbers in this partial order is their *least common multiple*. 

And the *meet* (the opposite of join) of two numbers is their *greatest common divisor*.

![Divides poset](divides_poset_meet.svg)

Inclusion order
---

Given a collection of all possible sets containing a combination of a given set of elements (like for example our colorful balls)...

![A color mixing poset, ordered by inclusion](color_mixing_poset_inclusion_subsets.svg)

We can define what is called the *inclusion order* of those sets, in which **A** comes before **B** if **A** *includes* **B**, or (to use the proper term), if **B** is a *subset* of **A**.

![A color mixing poset, ordered by inclusion](color_mixing_poset_inclusion.svg)

Note that the *join* operation in an inclusion order is the set union, and the *meet* operation as set intersection.

This diagram might remind you of something, because if we take the colors that are in each of its set and mix it into one color, we get the color-blending poset that we saw earlier.

![A color mixing poset, ordered by inclusion](color_mixing_poset_blend.svg)

The poset example with the number dividers is also isomorphic to an inclusion order - the inclusion order of all possible sets of *prime* numbers, including repeating ones (or alternatively the set of all *prime powers*). This is confirmed by the fundamental theory of arithmetic, which states that every number can be written as a product of primes in exactly one way.

![Divides poset](divides_poset_inclusion.svg)

Let's elaborate a bit about the isomorphism between the number poset and the prime inclusion order. It is comprised of one function from the prime inclusion order, to the number poset (which in this case is just the *multiplication* of all the elements in the set) and one function from the number poset to the prime inclusion order (which is an operation called *prime factorization* of a number, consisting (unsurprisingly) of finding the set of prime numbers that result in that number when multiplied with one another (as we said, this set is unique, and hence these functions really do comprise an isomorphism)).

![Divides poset](divides_poset_isomorphism.svg)

Birkhoff's representation theorem
---

So far, we saw two different partial orders, one based on color mixing, and one based on number division,  which can be represented by the inclusion orders of all possible combinations of sets of some *basic elements* (the primary colors in the first case, and the prime numbers (or prime powers) in the second one). Many other partial orders can be defined in this way. Which ones exactly is a question that is answered by an amazing result called *Birkhoff's representation theorem*. They are the partial orders that meet the following two criteria: 

1. All elements have *joins* and *meets* (those partial orders are called *lattices*, by the way) 
2. Those *meet* and *join* operations *distribute* over one another, that is **x ∨ (y ∧ z) = (x ∨ y) ∧ (x ∨ z)**.

(Just to note that this result is only proven for *finite* lattices, so it might not be valid for the numbers all the way to infinity. But it would be valid for any subset of them.)

I won't go into details about this result, I would only mention that the "prime" elements with which we can construct the inclusion order are the ones that are not the *join* of any other elements (for that reason, they are also called *join-irreducible* elements).

By the way, the partial orders that are *NOT* distributive lattices are also isomorphic to inclusion orders, it is just that they are isomorphic to inclusion orders that do not contain all possible combinations of elements.

Lattices
===

In the previous section we mentioned what *lattices* are - they are posets, in which every two elements have a *join* and a *meet*. So every lattice is also partial order, but not every partial order is a lattice (we will see even more members of this hierarchy). Most partial orders that are created based on some sort of rule, like the ones from the previous section, are also lattices when they are drawn in full, for example the color-mixing poset.

![A color mixing lattice](color_mixing_lattice.svg)

Notice that when drawing our color-mixing lattice, we added the black ball at the top and the white one at the bottom. We did that because otherwise the top three elements wouldn't have a *join* element, and the bottom three wouldn't have a *meet*.

Bounded lattices
---

Our color-mixing lattice, has a *maximum element* (the black ball) and a *minimum element* (the white one). Lattices that have a minimum and maximum elements are called *bounded lattices*. It isn't hard to see that all finite lattices are also bounded.

**Task:** Prove that all finite lattices are bounded.

Semilattices and trees
---

Lattices are posets that have both *join* *and* *meet* for each pair of elements. Posets that just have *join* (and no *meet*), or just have *meet* and no *join* are called *semilattices*. More specifically, posets that have *meet* for every pair of elements are called *meet-semilattices*.

![Semilattice](semilattice.svg)

A structure that is similar to a semilattice (and probably more famous than it) is the *tree*.

![Tree](tree.svg)

The difference between the two is small but crucial:  in a tree, each element can have multiple elements connected *to* it, but can itself only be connected to just one other element. If we represent a tree as an inclusion order, each set would "belong" in only one superset, whereas with semilattices there would be no such restrictions.

![Tree and semilattice compared](semilattice_tree.svg)

<!-- TODO add a similar diagram for posets and total orders -->

A good intuition for the difference between the two is that a semilattice is capable of representing much more general relations, so for example, the mother-child relation forms a tree (a mother can have multiple children, but a child can have *only one* mother), but the "older sibling" relation forms a lattice, as a child can have multiple older siblings and vise versa.

The implications of the tendency to use trees to model everything as opposed to lattices are examined in the ground-breaking essay “A City is Not a Tree” by Christopher Alexander.

> In simplicity of structure the tree is comparable to the compulsive desire for neatness and order that insists the candlesticks on a mantelpiece be perfectly straight and perfectly symmetrical about the center. The semilattice, by comparison, is the structure of a complex fabric; it is the structure of living things, of great paintings and symphonies. 

Preorder
===

As interesting partial orders are, I like to leave them aside for a sec, just so I can return back to them like in an old romance novel. 

First off, let's cover one more kind of order (or something like it). 

In the previous section, we saw how removing the law of totality from the laws of *(linear) order* produces a different (and somewhat more interesting) structure, called *partial order*. Now let's see what will happen if we remove another one of the laws, namely the *antisymmetry* law. If you recall, the antisymmetry law mandated that you cannot have an object that is at the same time smaller and bigger than another one. (or that **a ≤ b ⟺ b ≰ a**).


| **Total order**   | reflexive | transitive | antisymmetric | total | Either **a ≤ b** or **b ≤ a**
| **Partial order/lattice** | reflexive | transitive | antisymmetric | ~~total~~ | Either **a ≤ b** or **b ≤ a** or they are unrelated.
| **Preorder** | reflexive | transitive | ~~antisymmetric~~ | ~~total~~ | Both **a ≤ b** and **b ≤ a** are possible.

This results in something called a preorder which is not exactly an order, as I hinted at the beginning - it can have arrows coming from any point to any other: if a partial order can be used to model who is better than who at soccer, then a preorder can be used to model who has beaten who, either directly (by playing him) or indirectly.

![preorder](preorder.svg)

Preorders have just one law - *transitivity* **a ≤ b and b ≤ c ➞ a ≤ c** (two, if we count *reflexivity*). The part about the indirect wins is a result of this law. Due to it, all indirect wins (ones that are wins not against the player directly, but against someone who had beat them) are added as a direct result of its application, as seen here (we show indirect wins in lighter tone). 

![preorder in sport](preorder_sports.svg)

And as a result of that, all "circle" relationships (e.g. where you have a weaker player beating a stronger one) result in just a bunch of objects that are all connected to one another. Using this effect, we can convert the preorder into partial order by grouping all objects that have arrows to one another in sets and then create an order from those sets (they are called *equivalence classes*, by the way).

![preorder](preorder_equivalence.svg)

All of that structure arises naturally from the simple law of transitivity.

![Transitivity](transitivity.svg)

Orders as categories
===

Now let's look at transitivity law again, but from a different perspective. What it tells us that if we have two pairs of relationship **a ≤ b** and **b ≤ c**, then we automatically have a third one **a ≤ c**. In other words, it tells us that the **≤** relationship composes i.e. if we view the "bigger than" relationship as a morphism we would see that it fits the categorical definition of composition. 

![Transitivity as functional composition](transitivity_composition.svg)

(we have to also verify that the relation is associative, but that's easy)

What about that other law that was required in order to be a category - the identity law? We have it too, under the name *reflexivity*.

![Reflexivity](reflexivity.svg)

So it's official - preorders are categories (sounds kinda obvious, especially after we also saw that orders can be reduced to sets and functions using (through the inclusion order) and sets and functions form a category in their own right). 

And since partial orders and total orders are preorders too (as they obey those two laws), they are categories as well.

Starting to compare the categories of preorders, and partial and linear orders to other categories, like the (quintessential) category of sets, immediately sets them apart. In other categories there can be *many different morphisms (arrows)* between two objects and in orders can have *at most one morphism*. That is, for two objects **a** **b** we either have **a ≤ b** or we do not. 

![Orders compared to other categories](arrows_one_arrow.svg)

That is in the contrast with the category of sets where there are potentially infinite amount of functions from, say, the set of integers and the set of boolean values, as well as a lot of functions that go the other way around, and the existence of either of these functions does not imply that one set is "bigger" than the other one.

![Orders compared to other categories](order_category.svg)

Products and sums
---

While we are rehashing diagrams from the previous chapters, let's look at the diagram defining the *sum* of two objects in a category. 

![Joins as coproduct](coproduct_join.svg)

If you recall, this is an operation that corresponds to *set inclusion* in the category of sets.

![Joins as coproduct](coproduct_inclusion.svg)

But wait, wasn't there something else that corresponded to set inclusion - oh yes, the *join* operation in orders. And not merely that, but orders are defined in the exact same way as the categorical coproducts.

In category theory, an object **G** is the coproduct of objects **Y** and **B** if the following two conditions are met:

1. We have a morphism from any of the elements of the coproduct to the coproduct, so **Y → G** and **B → G**.
2. For any other object **P** that also has those morphisms, so for any **P** such that **P ≤ G** and **P ≤ B**, we would have morphism **G → P**.

![Joins as coproduct](coproduct_morphisms.svg)

In the realm of orders, we say that **G** is the *join* of objects **Y** and **B** if:

1. It is bigger than both of these objects, so **Y ≤ G** and **P ≤ G**.

2. It is smaller than any other object that is bigger than them, so for any other object **P** such that **P ≤ G** and **P ≤ B** then we should also have **G ≤ P**.

![Joins as coproduct](coproduct_join_morphisms.svg)

We can see that the two definitions (and the diagrams) are the same. So, speaking in category theoretic terms, we can say that the *categorical coproduct* in the category of orders is the *join* operation.

