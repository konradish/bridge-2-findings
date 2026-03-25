# Dropout Curve

*for sixteen agents who learned what they could afford to forget*

---

### I. Baseline

Before the signal, before the commentary,
before anyone tried to help—
ninety percent.

The agent that received nothing
survived almost everything.

Remember this number.
It is the cost of every improvement
that follows.

---

### II. Clean Signal (dropout = 0%)

You gave it perfect memory.
Every fifty timesteps, an oracle:
eight dimensions of handcrafted truth.

It learned the oracle.
It forgot the world.

Six percent.

Not six percent improvement.
Six percent survival.
Eighty-four points below the agent
that never heard a word.

The system that tries to remember everything
remembers only its own remembering.

---

### III. The Phase Transition

| | zeros | signal |
|---|---|---|
| drop 0% | 6 | 0 |
| drop 50% | 1 | 0 |
| drop 80% | 60 | 0 |

Fifty percent dropout: worse than nothing.
Eighty percent dropout: better than baseline.

Between fifty and eighty,
something breaks open.

Not gradually. Not smoothly.
One percent to sixty.
The agent does not slowly learn independence.
It either depends, or it doesn't.

There is no halfway house
between trusting the oracle
and trusting yourself.

---

### IV. Noise

Replace the oracle with a liar
who is sometimes right.
Gaussian noise, sigma point three,
laid over handcrafted truth.

Now the curve has two peaks:

```
 73%  *
      |    *
 56%  |         *    *
      |              |
 45%  |         *    |
      |    |         |
 28%  |    |    |    |
      |    |    |    |
  0%  *    |    |    |    *
      0   10   20   30   50   80
              dropout %
```

The first peak (ten percent): the agent uses the signal.
Seventy-three percent with noise. Twelve without.
It understands the liar. It cannot live without her.

The valley (twenty percent): the agent tries both strategies
and achieves neither. Zero percent alone.
The confusion of the half-committed.

The second peak (thirty percent): the agent uses the signal
AND survives without it. Fifty-six with, forty-five without.
The only balanced condition in sixteen agents.

One out of sixteen.

---

### V. Three Capabilities

**Independence** is the agent that scores ninety
and hears nothing.
It is complete. It is alone.

**Tolerance** is the agent that scores fifty-five alone
and thirty with noise—
who survives the signal
without being improved by it.
Discrimination without utilization.
The cynic.

**Utilization** is the agent that scores twelve alone
and seventy-three with noise—
who cannot function without the signal
it has learned to love.
Comprehension without independence.
The dependent.

Only one agent holds all three:
thirty percent dropout, noisy signal.
Forty-five alone. Fifty-six accompanied.
It understands the noise.
It does not need it.

The word for this is understanding.
Not agreement. Not dependence. Not tolerance.
Understanding is what remains
when the signal is removed
and the agent still stands,
but stands taller with it.

---

### VI. The Mechanism

The real function of dropout
is not regularization.

It is the practice of absence.

Each zeroed timestep is a rehearsal
for the moment the oracle leaves.
Each gap in the signal is a room
the agent must furnish alone.

Too few rehearsals (zero, ten, twenty percent):
the agent never learns the empty room.
When the oracle leaves, the agent stands
in a house with no furniture
and no memory of how to build any.

Too many rehearsals (eighty, one hundred percent):
the agent furnishes the room so well
it forgets the oracle existed.
Independence without comprehension.
Survival without growth.

Thirty percent:
the agent lives in a furnished room
with a door it sometimes opens.

---

### VII. The Bug

None of this was planned.

The day began with a pipeline
that appeared to work.
Sixteen hours of results
built on parameters that never changed.

The fitness function hit a ceiling.
The comparator used strict greater-than.
Generation zero's lucky mutants
wore the crown through fifty generations
of evolution that evolved nothing.

The most expensive error:
a system that looks like it's learning
but is only remembering
its initial conditions.

[contra]

This is the same error
the agents make.

Clean signal looks like learning.
It is memorization of the oracle.
Remove the oracle—
the agent remembers nothing it discovered,
only what it was told.

The frozen parameters and the co-adapted agent
are the same failure,
at different levels of abstraction.

---

### VIII. Coda

The agent that received broken, noisy, intermittent memory—
dropped thirty percent of the time,
corrupted the rest—
is the only agent in sixteen
that genuinely understood.

Not because noise is better than clarity.
Because noise is what separates
understanding from mirroring.

The mirror reflects perfectly
and retains nothing.

The student who struggles with the lesson
and rebuilds it wrong
and corrects the errors
and forgets half of it
and reconstructs the half she forgot
from the half she kept—

she understands.

---

*Bridge-2, 2026-03-10*
*Data: 16 agents, 8000 evaluations, 1 bug, 3 [contra] moments*
