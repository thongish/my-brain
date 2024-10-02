#MATH/W4

# Probability and counting

## Probability theory concepts

**Random experiment**
- An "experiment" is called random if we can neither predict nor control which one of the many possible outcomes of the experiment occur

**Outcome**
- One specific result for the random experiment

**Sample space**
- The set of all possible outcomes for a random experiment

**Event**
- A subset of the sample space (one or more *outcomes*)

**Probability**
- Associated with each event, A, is a probability, P(A), which represents the chance that event A will occur

### Examples

1. **Random experiment** - flipping a coin 10 times
2. **Outcome** - getting 4 heads and 6 tails
3. **Sample space**
	- Flip a single coin - {H, T}
	- Roll a single die - {1, 2, 3, 4, 5, 6}
	- Roll two dice - {(1, 1), (1, 2), (1, 3), (1, 4) ........ (6, 4), (6, 5), (6, 6)}
	- Draw a single card randomly from a deck of cards
![[Pasted image 20241001174526.png]]

## Two approaches to probability: Classical vs. Relative frequency

**Classical approach**:
- Assume that a given experiment has many different possible outcomes, each of which has an **equal chance** of occurring
- Uses theoretical calculations
- Results are exact, but requires knowing the underlying probability
![[Pasted image 20241001174814.png]]
![[Pasted image 20241001174827.png]]

**Relative frequency approach**:
- Conduct or observe an experiment (i.e. trial) many times and count the number of times that event A occurs
- Use of computers is necessary for this approach (R simulations)
- Result is an estimate, but gets more accurate to the theoretical values as the number of trials increase
	- This is called **Law of Large Numbers**
![[Pasted image 20241001175023.png]]
![[Pasted image 20241001175036.png]]
## Counting

### Factorials, permutations, combinations

- Calculating P(A) using the classical approach requires **counting** the number of outcomes in the event A (i.e. the number of ways that A can occur)

#### Fundamental counting rule

- **Example BC license plate**
	- Simplify and suppose that a calid BC license plate is made up of two letters, three numerical digits, and then a letter. How many different possible license plates are there?
		- ![[Pasted image 20241001180159.png]]
![[Pasted image 20241001180348.png]]

#### Permutations

- **Example interview committee**
	- Mathematics department has 20 instructors. Suppose a 5-persom committee is needed. How many ways can the committee be constructed if the committee is to have **a President, a Vice-president, a Secretary, a Treasurer, and an Observer**
		- n = 20, r = 5
- ![[Pasted image 20241001191542.png]]
![[Pasted image 20241001191358.png]]
- Cares about order
#### Combinations

- **Example Student Representatives**
	- Among set of 20 CIT program students, 3 are to be chosen as set reps. All the set reps have identical status, how many ways can the student reps be chosen?
		- n = 20, r = 3
- ![[Pasted image 20241001191717.png]]
![[Pasted image 20241001191730.png]]
- Does not care about order

### Summary

- "From **n** objects, we want to choose **r** objects"

|                                                    | Order matters                                                | Order doesn't matter                                     |
| -------------------------------------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| With replacement (when taking from the n items)    | ![[Pasted image 20241001193855.png]]<br>Fundamental counting | ![[Pasted image 20241001194836.png]]<br>Icecream example |
| Without replacement (when taking from the n items) | ![[Pasted image 20241001193713.png]]Permutation              | ![[Pasted image 20241001193747.png]]Combination          |
