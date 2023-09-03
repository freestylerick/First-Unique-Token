# First-Unique-Token

A very quick and messy possible solution to Callum McDougall's august 2023 transformer interp problem.

https://arena-ch1-transformers.streamlit.app/Monthly_Algorithmic_Problems --> [August] First Unique Token


# From char.ipynb:

very rough guess. code [] is nasty - no expectations of you reviewing my code:

H0.1) - finds when two letters match, off of the main diagonal - but misses 'a' matches H0.0) - copies all letters, in order, to shared memory (duplicate letters with self are not copied however; self is also not copied, but this is ok because self exists as the original element of the resid stream). qtok-kpos subcircuit shows that letters will be ordered in this shared memory from left to right - so we can selected an ordered one later if desired. H0.2) - finds when some specific letters match, off of the main diagonal - specifically, gets 'a' (which was missed in H0.1). as well as 'b' and 'g'. This head might also be doing something that looks similar to H0.0 - either in the same direction or opposite direction.

Note that this hypothesized Layer 0 mechanism is pretty reasonable without layer 1. It gets all sequences of lengths 1 - 3 correct.
It gets all sequences when the first letter doesn't repeat correct (by suggesting the first letter). It gets all sequences when the current letter matches the first letter and the second letter doesn't repeat correct (by suggesting the second letter).

The thing missing is a component the discourages a repeating letter when that letter isn't the last letter. This is what layer 1 does. (I think). H1.0) discourages 'a' and 'c' when they repeat. H1.1) discourages 'd','e', 'f', and 'j' when they repeat. possibly slight discouragement on 'i' when it repeats H1.2) discourages 'b','g', 'h', and 'i' when they repeat.
Each letter is hit by 1 head.

Note that this discouragement combined with H0.0) allows a theoretically optimal mechanism to get the correct letter.

The mechanism isn't optimal though, layer 1 discouragement seems to sometimes fight with itself along the same head when it wants to discourage multiple letters. I think it's also weaker as window gets longer.
