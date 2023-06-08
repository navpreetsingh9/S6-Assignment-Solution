# S6-Assignment-Solution



Steps :

1. Add formulas for each layer. 

   1. Input layer i1, i2 is already given. 

   2. Output layer t1 and t2 is already given for an example. 

   3. Using weighted connections write down the formulas for first layer output h1,h2,a_h1,a_h2 using weights w1,w2,w3,w4 connection.

      | h1 = w1*i1 + w2*i2              |
      | ------------------------------- |
      | h2 = w3*i1 + w4*i2              |
      | a_h1 = σ(h1) = 1/(1 + exp(-h1)) |
      | a_h2 = σ(h2)                    |

   4.  Similarly o1,o2,a_o1,a_o2 using weights w5,w6,w7,w8. 

      | o1 = w5*a_h1 + w6*a_h2 |
      | ---------------------- |
      | o2 = w7*a_h1 + w8*a_h2 |
      | a_o1 = σ(o1)           |
      | a_o2 = σ(o2)           |

   5. Also write the formula for loss of each output E1 by comparing t1 and a_o1 and calculating mean square distance and similarly for E2.

      | E1 = ½ * (t1 - a_o1)² |
      | --------------------- |
      | E2 = ½ * (t2 - a_o2)² |

   6.  Finally total loss which is sum of E1 and E2.

      | E_total = E1 + E2 |
      | ----------------- |
      |                   |

2. Calculate partial derivative of total loss with respect of each weight using chain rule of their connections as going through forward propagation. 

   1. So partial derivative of total loss wrt w5 = partial derivative of E1 wrt a_o1 * partial derivative of a_01 wrt o1 * partial derivative of o1 wrt w5. 

      | ∂E_total/∂w5 = ∂(E1 + E2)/∂w5                        |
      | ---------------------------------------------------- |
      | ∂E_total/∂w5 = ∂E1/∂w5                               |
      | ∂E_total/∂w5 = ∂E1/∂w5 = ∂E1/∂a_o1*∂a_o1/∂o1*∂o1/∂w5 |

   2. Using formula from step 1, calculate partial derivative of each. 

      | ∂E1/∂a_o1 =   ∂(½ * (t1 - a_o1)²)/∂a_o1 = (a_01 - t1) |
      | ----------------------------------------------------- |
      | ∂a_o1/∂o1 =   ∂(σ(o1))/∂o1 = a_o1 * (1 - a_o1)        |
      | ∂o1/∂w5 = a_h1                                        |

   3. Calculate similarly for the weights w6,w7,w8. 

      | ∂E_total/∂w5 = (a_01 - t1) * a_o1 * (1 - a_o1)  * a_h1 |
      | ------------------------------------------------------ |
      | ∂E_total/∂w6 = (a_01 - t1) * a_o1 * (1 - a_o1) * a_h2  |
      | ∂E_total/∂w7 = (a_02 - t2) * a_o2 * (1 - a_o2) * a_h1  |
      | ∂E_total/∂w8 = (a_02 - t2) * a_o2 * (1 - a_o2) * a_h2  |

   4. Also partial derivative of total loss wrt w1 =  partial derivative of total loss wrt a_h1 (for both E1 and E2 loss) *  partial derivative of a_h1 wrt h1 *  partial derivative of h1 wrt w1. 

      | ∂E1/∂a_h1 = (a_01 - t1) * a_o1 * (1 - a_o1) * w5             |
      | ------------------------------------------------------------ |
      | ∂E2/∂a_h1 = (a_02 - t2) * a_o2 * (1 - a_o2) * w7             |
      | ∂E_total/∂a_h1 = (a_01 - t1) * a_o1 * (1 - a_o1) * w5 + (a_02 - t2) * a_o2 * (1 - a_o2) * w7 |
      | ∂E_total/∂a_h2 = (a_01 - t1) * a_o1 * (1 - a_o1) * w6 + (a_02 - t2) * a_o2 * (1 - a_o2) * w8 |

   5. Similarly calculate for w2,w3,w4

      | ∂E_total/∂w1 = ∂E_total/∂a_h1 * ∂a_h1/∂h1 *  ∂h1/∂w1 |
      | ---------------------------------------------------- |
      | ∂E_total/∂w2 = ∂E_total/∂a_h1 * ∂a_h1/∂h1 * ∂h1/∂w2  |
      | ∂E_total/∂w3 = ∂E_total/∂a_h2 * ∂a_h2/∂h2 * ∂h2/∂w3  |
      | ∂E_total/∂w4 = ∂E_total/∂a_h2 * ∂a_h2/∂h2 * ∂h2/∂w4  |

      | ∂E_total/∂w1 = ((a_01 - t1) * a_o1 * (1 - a_o1) *  w5 + (a_02 - t2) * a_o2 * (1 - a_o2) *  w7) * a_h1 * (1 - a_h1) * i1 |
      | ------------------------------------------------------------ |
      | ∂E_total/∂w2 = ((a_01 - t1) * a_o1 * (1 - a_o1) * w5 + (a_02 - t2) * a_o2 * (1 - a_o2) * w7) *  a_h1 * (1 - a_h1) * i2 |
      | ∂E_total/∂w3 = ((a_01 - t1) * a_o1 * (1 - a_o1) * w6 + (a_02 - t2) * a_o2 * (1 - a_o2) * w8) *  a_h2 * (1 - a_h2) * i1 |
      | ∂E_total/∂w4 = ((a_01 - t1) * a_o1 * (1 - a_o1) * w6 + (a_02 - t2) * a_o2 * (1 - a_o2) * w8) *  a_h2 * (1 - a_h2) * i2 |

3. Using the above equations calculate for 100 epochs and get final weights and loss after training.





### Screenshot of Excel sheet of Backpropagation

![Backpropagation Screenshot](https://github.com/navpreetsingh9/S6-Assignment-Solution/blob/73575741529836e43364d3b8db5dc05a7770d35e/img/Excel%20Screenshot.jpg "Screenshot")

### Graph of different Learning Rates

1. lr = 0.1

   ![LR = 0.1](https://github.com/navpreetsingh9/S6-Assignment-Solution/blob/73575741529836e43364d3b8db5dc05a7770d35e/img/lr1.jpg "LR = 0.1")

2. lr = 0.2

   ![LR = 0.2](https://github.com/navpreetsingh9/S6-Assignment-Solution/blob/73575741529836e43364d3b8db5dc05a7770d35e/img/lr2.jpg "LR = 0.2")

3. lr = 0.5

   ![LR = 0.5](https://github.com/navpreetsingh9/S6-Assignment-Solution/blob/73575741529836e43364d3b8db5dc05a7770d35e/img/lr3.jpg "LR = 0.5")

4. lr = 0.8

   ![LR = 0.8](https://github.com/navpreetsingh9/S6-Assignment-Solution/blob/73575741529836e43364d3b8db5dc05a7770d35e/img/lr4.jpg "LR = 0.8")

5. lr = 1.0

   ![LR = 1.0](https://github.com/navpreetsingh9/S6-Assignment-Solution/blob/73575741529836e43364d3b8db5dc05a7770d35e/img/lr5.jpg "LR = 1.0")

6. lr = 2.0

   ![LR = 2.0](https://github.com/navpreetsingh9/S6-Assignment-Solution/blob/73575741529836e43364d3b8db5dc05a7770d35e/img/lr6.jpg "LR = 2.0")
