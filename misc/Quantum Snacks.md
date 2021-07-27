# Quantum Snacks

## Challenge information:
   Computers speak the language of binary (zeros and ones), and every computer program is basically just applying logic gates (e.g NOT, OR, AND, XOR etc) to these bit to get a desired outcome. The important point here is to remember that a bit is a single variable that can have one of 2 values, either zero or one).
   
   Quantum computers speak a very different language. Instead of a bit we have a qubit (quantum bit), which can be represented as a two-dimensional vector. Classical bit 0 is equivalent to the qubit  ![CodeCogsEqn](https://user-images.githubusercontent.com/17177071/127027324-55d8c329-a9ba-430b-aacc-1fdb7636e81d.png)
, and the classical bit 1 is equivalent to the qubit  ![CodeCogsEqn2](https://user-images.githubusercontent.com/17177071/127027356-a3eec64c-cac9-44cb-aa98-e11144bcbcc7.png)
, but there are many other qubit states that do not have a classical equivalence, which means that qubits can store much more information than classical bits. The goal of this challenge is to understand this concept better.

   To change the state of a (q)bit we apply logic gates to it. In quantum computing logic gates are represented as matrices, and the outcome of this operation can be calculated by multiplying the logic gate (a matrix) with the initial qubit state (a vector). Mathematically it looks like this:
   
   ![CodeCogsEqn3](https://user-images.githubusercontent.com/17177071/127027509-84063b87-c3c7-4a62-b0fe-5b5105b7d339.png)
   
   In this challenge we limit ourselves to three 1-qubit logic gates:
   
   ![CodeCogsEqn4](https://user-images.githubusercontent.com/17177071/127027551-638b48a2-0429-4b82-b02e-58d69d1a8fc0.png)

   Note: in practice there are more logic gates that result in an infinite possible quantum states. Because we are only considering 3 specific logic gates then the number of states is finite.

### Flag 1 [50 points]:
####   How many states?

####   Description:
  Considering only these 3 logic gates, and starting in the (1, 0) state, how many states can the qubit have? Hint: Start applying the logic gates in random order. Drawing the result in x-y coordinates will greatly help you understand the result. 

####   Solution:
  Actually I didn't know actual soluton. I was too lazy to make the math for all of this and I just bruteforced the site by hand. 
  I was distracted by communicating with the team during bruteforcing and when it was solved I didn't pay attention to what number I trying (my hands did it automatically).
  But I do remember the number was between 80 and 100 :D

### Flag 2 [50 points]:
####   Make a circuit

####   Description:
  Provide a circuit (a series of operations) that transforms the state ![CodeCogsEqn](https://user-images.githubusercontent.com/17177071/127027624-fbc23c5d-931b-46e9-af3c-ab6c3954114f.png)
 to the state ![CodeCogsEqn5](https://user-images.githubusercontent.com/17177071/127027642-c5b8afde-12dd-4bc0-945d-593f23199e8b.png)
, only using the H and X operations. A possible (wrong) answer is HHXHXHXH.

####   Solution:
  First of all, I tried to really understand what these gates do to the qbits. This is what I understood:
    X just flips the qbit. Example: was (1, 0), then (0, 1)
    Z just multiplies the lower bit to -1. Example: was (1, 1), then (1, -1)
    H is the weirdest gate. It is multiply lower bit to -1 and every bit to 1/sqrt(2). Example: was (1, 1), then (1/sqrt(2), -1/sqrt(2)). If bit is 1/sqrt(2) it makes it 1.
  
  So to get from (1, 0) to (-1, 0) we must flip qbit (X (0, 1)), then make the lower bit negative (H (0, -1/sqrt(2))), then flip it again with (X (-1/sqrt(2), 0)) and get rid of this square root term (H (-1, 0))

  Right sequence: XHXH
  **FLAG: CTF{quantum_circuit_master} **


### Flag 3 [50 points]:
####   Short circuit
   
####   Description:
  Same as question 2 but now provide the shortest circuit possible (minimal number of gates). You are allowed to use H, X and Z.
  So first we flip with (X, (0, 1)), then we multiply with -1 by (Z, (0, -1)), and we flip again with (X, (-1, 0))

####   Solution:
  Since we have the gate that makes the lower bit negative we don't have to deal with 1/sqrt(2). 

  Right sequence: XZX
  
  **FLAG: XZX**
