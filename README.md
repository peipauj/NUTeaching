# NUTeaching

# Revenue Management

## Chapter 0: Review of LP and DP

### Review of Linear Programming
A linear programming is an optimization of a linear objective function over a convex set. The convex set is called polyhedron that is the intersection of finite number of half-spaces. If the conex set is feasible, then it has at least one extreme point and further if the optimization problem has a finite optimal solution , it must be attained at one of the extrement points as shown below.
#### Problem formulation in standard form
Every linear programming can be written in the following standard form:<br><br>
Minimize: $\quad CX $ <br>
subject to:$\quad AX=b $<br>
 $\quad \quad \quad \quad$ $X\ge 0$. <br><br>
Vector $C$ is the cost coefficients. Matrix $A$ is the coefficients of linear contraints and $b$ is right-hand terms. The set $P=\{x\in \Re^n:Ax=b,x\ge 0\}$ is convex and define a polyhedron.
#### Fundamental theorem of linear programming
Let $P=\{x:Ax=b,x\ge 0\}$. If $A$ is of full rank and $\underset{x\in P}{max} \{cx\}$ has a finite optimal solution, there is an optimal solution at one of the extreme points of $P$.

#### Example

There are $m$ flight resources with capacity $c_i>0$ for each resource $i$. Combining flight origin, destination and fare class, we have $n$ ODF. We assume $m<n$ so each resource used in at least 1 ODF. The incidence matrix $A$ has elements $a_{i,j}$ as follows.
$$
a_{i,j} = \left\{
        \begin{array}{ll}
            1 & \quad \text{if resource $i$ used in product $j$}\\
            0 & \quad \text{Otherwise.}
        \end{array}
    \right.
$$


The decisions $x_j$ to make are how many seats to sell for each ODF $j$. Suppose there are 2 resources: flight from San Francisco to Denver and Denver to St. louis and 2 fare classes: full and discount. Then we have total 6 ODF. The revenue terms are $p_j$ for each unit sale of product $j$. We assume demand are known as $d_j$ for each ODF. The revenue maximization can be formulated as follows.<br><br>
Maximize: $\overset{6}{\underset{j=1}{\Sigma}}P_jX_j $ <br>
subject to :$\overset{6}{\underset{j=1}{\Sigma}} a_{i,j}X_j \le c_i \quad \forall i$<br>
 $\quad \quad \quad $ $X_j\le d_j \quad \forall j$<br>
 $\quad \quad \quad $ $X_j\ge 0 \quad \forall j$.<br>

#### Discussion 
1. known deterministic demand $d_j$ : Deterministic LP ignores the uncertainty in real demand.
2. The LP doesn't model the dynamics of the demand. Its solution provides a partition-based booking policy that ignores the inter-relations among flight resources. In practice, the performance is not optimal.

#### Duality
Consider the standard form LP as follows and call it the primal problem.<br><br>
$\textbf{Primal}$<br>
Minimize: $\quad CX $ <br>
subject to:$\quad AX=b $<br>
 $\quad \quad \quad \quad$ $X\ge 0$. <br><br>
 Assume an optimal solution exists and call it $x^*$. We introduce a relaxed problem to the primal by replacing the constraint with a penalty term in the objective function as follows.<br> <br>
 $\textbf{Primal relaxation}$<br>
 Minimize: $\quad CX+p(b-Ax) $ <br>
subject to: $\quad \quad \quad \quad$ $X\ge 0$. <br><br>
let $g(p)$ be the optimal value to the primal relaxation that is a function of price vector $p$. As can be seen below, the primal relaxation allows more options and its optimal value is no larger than that in the primal problem.
$$g(p)=\underset{x\ge 0}{min}[cx+p(b-Ax)]\le cx^*+p(b-Ax^*)=cx^*$$
#### Formulation of dual to primal problem
 
Maximize: $\quad Pb$ <br>
subject to: $\quad PA \le C$. <br><br>
The vector $p$ is a price vector that corresponds to each linear constraints in the primal problem. Notice that non-negative constraints in primal problem correspond to the signs of the constraints in dual problem. <br><br>
In summary, we have the following formulation between priml and dual problems.<br>
\begin{array} {|r|r|} \hline 
Primal & Minimize & Maximize & Dual \\ \hline
Constrints &\ge b_i & \ge 0 &Variables \\
  &\le b_i & \le 0 & \\ 
 &=b_i & free & \\ \hline
Variables &\ge 0 & \le c_j &Constraints \\
 &\le 0 &\ge c_j & \\ 
  &free &= c_j & \\ \hline
\end{array}
#### Example
Continue the same airline example above. It is popular in practice to book flights by bid prices. That is, a demand is accepted given the demand of class $j$ is no lower than sum of the bid price of required resources of class $j$. We formulate the dual to the primal problem above and calculate the bid prices.<br><br>
Minimize: $\overset{2}{\underset{i=1}{\Sigma}}p_i c_i +\overset{6}{\underset{j=1}{\Sigma}}q_jd_j $ <br>
subject to :$\overset{2}{\underset{i=1}{\Sigma}} a_{i,j}p_i+q_j\ge f_j \quad \forall j$<br>
 $\quad \quad \quad $ $q_j\ge 0 \quad \forall j$<br>
 $\quad \quad \quad $ $p_i\ge 0 \quad \forall i$.<br>
 In the dual problem, $p_i$ are dual prices corresponding to resource capacity contraints that are used in bid price policy. Dual variables $q_j$ are related to demand contraints in the primal.<bf><br>
 
We continue to review some important resutls in duality theory.<br>
$\mathbf{Lemma:}$ (1) If primal program is infeasible then its dual is either infeasible or unbounded. (2)If if the dual is unbounded then the primal is infeasible.<br><br>
Notice that there are just 3 cases in a linear programming problem: 1) Infeasible,2) finite optimal; and 3)unbounded.<br><br>
$\textbf{Weak duality theorem:}$ If primal problem is finite optimal, so is the dual and furhter $P^*b\le cx^*$,where $x^*$ and $p^*$ are primal and dual optimal solutions respectively.<br><br>
$\textbf{Strong duality theorem:}$ If feasible solutions for primal problem exist, then they are equal,i.e.,$P^*b=cx^*$.<br><br>
Notice that weak duality states that dual optimum is a lower bound on primal optimum. Strong duality further says the bound is tight.
### Review of Dynamic Progeamming

Fundamentally, dynamic programming addresses how to make optimal decisions over time. In nature, it can be both stochastic and deterministic. In this revie,we focus on stochastic program and summarize the key results. <br><br>

There are $T$ periods. Time is indexed by $t$. <br>

1. System state: $x(t)$ assumed to be discrete and constrained in a finite set $S_t$.<br>
2. Control system: $u(t)$ assumed to be discrete and constrined in a finite set $U_t(x(t))$.<br>
3. Random disturbance: $w(t))$ assumed to be discrete random variable/vector with known distribution. They are independent over time.<br>
4. System function: $f_t(x(t),u(t),w(t))$ determines the next state as a function of current state, decisions and disturbance by $x(t+1)=f_t(x(t),u(t),w(t))$.<br>
5. Reward function: $g_t(x(t),u(t),w(t))$ assumed to be real-valued function of current state, decisions and disturbance. The total reward is additive as follows. $$g_{T+1}(x(T+1)+\overset{T}{\underset{t=1}{\Sigma}}g_t(x(t),u(t),w(t)).$$ <br><br>
6. Control policy: ${u_1,u_2,...,u_T}$ is a collectin of actions. It is admissive if $u(t)\in \mathbb U(x(t)).$<br>

The objective of the dynamic programm is to maximize the total expected reward below by choosing control actions $u(t)$ over time.

$$\mathbb E[g_{T+1}(x(T+1)+\overset{T}{\underset{t=1}{\Sigma}}g_t(x(t),u(t),w(t))].$$


The expected reward of a control policy $\mu$ is as follows.

$$V_1^{\mu}(x)=\mathbb E[g_{T+1}(x(T+1)+\overset{T}{\underset{t=1}{\Sigma}}g_t(x(t),\mu(t),w(t))].$$

An optimal policy $\mu^*$ is one for which $V_1^{\mu^*}=\underset{\mu\in \mathbb M}{Sup} \quad V_1^{\mu}(x).$ The optimal expected reward is denoted by $V_1(x).$

### The principle of optimality

The principle of optimality lies at the heart of dynamic programming. It basically says that if a policy is optimal for the original problem above then it must be optimal fo any subproblem of this same original problem. <br><br>

We define the reward-to-go for policy $\mu$ at time $t$ by 

$$V_t^{\mu}(x)=\mathbb E[g_{T+1}(x(T+1)+\overset{T}{\underset{s=t}{\Sigma}}g_s(x(s),\mu(s),w(s))| x(t)=x].$$<br><br>

$\mathbf{Therem}$: If policy $\mu^*=\{\mu_1^*,\mu_2^*,...,\mu_T^*\}$ is an optimal policy for the dynamic program define above, then truncated policy $\{\mu_t^*,\mu_{t+1}^*,...,\mu_T^*\}$ is optimal for the t-subproblem. That is,<br><br>
$$V_t^{\mu^*}(x)=\underset{\mu\in \mathbb M}{Sup} \quad V_t^{\mu}(x)\quad \forall x\in S_t.$$

### The dynamic programming recursion

The principle of optimality leads to a recursion procedure for finding optimal plicy. We define optimal reward-to-go as follows, which is also called value function.
$$V_t(x)=\underset{\mu\in \mathbb M}{Sup} \quad V_t^{\mu}$$ <br><br>

$\mathbf{Proposition}$: The value function $V_t(x)$ is the unique solution to the recursion below<br><br>
$$V_t(x)=\mathbb E[g_{T+1}(x(T+1)+\overset{T}{\underset{s=t}{\Sigma}}g_s(x(s),\mu(s),w(s))| x(t)=x],$$ for all $t$ and all $x\in S_t$ with boundary condition $V_{T+1}(x)=g_{T+1}(x), \forall x\in S_{T+1}.$
Moreover, if $\mu^*=\mu_t^*(x)$ achieves the maximum in above, then $\mu=\{\mu_1^*,\mu_2^*,...,\mu_T^*\}$ is an optimal policy.<br><br>

### Systems with observable disturbances

Consider the case in which we determine actions based upon perfect knowledge of the disturbance $w(t)$ in each time $t$. In other words, we allow the decision to be a function of both system state $x(t)$ and random disturbance $w(t)$. The idea is that in this situation we can observe the disturbance before making our decision.
<br>
 
 In this case, the basic dynamic programming recursion becomes
 $$V_t(x)=\underset{\mu(x,w(t))\in \mathbf U_t(x)}{max} \quad E[g_t(x,\mu(t,w(t)),w(t))+V_{t+1}(f_t(x,\mu(x,u(x,w(t)),w(t)))].$$<br><br>
 Since we can choose a control decision  based upon knowing $w(t)$, the recursion can be rewritten as 
$$V_t(x)=E[\underset{\mu\in \mathbf U_t(x)}{max} \quad g_t(x,\mu,w(t))+V_{t+1}(f_t(x,\mu,w(t))].$$<br><br>

The recursion above has switched $E[max\{\}]$ with $max \{E[]\}$ because optimal decision $\mu_t(x)$ in time $t$ can be chosen based upon each realized random term $w(t)$. By using this transformation we have reduced the state space from $S_t\times W_t$ in original DP problem to $S_t$ in the reduced-form DP.<br><br>

### Application of dynamic program in revenue management

Here is a typical example of how this transformation applies in RM. Suppose $x(t)$ is a scalar capacity, $y(t)$ is the revenue of the request in period $t$, and $\mu(t)=1$ if we decide to accept a request and $0$ otherwise. The reward function is simply $y(t)u(t)$. Capacity as a system state evolves according to $x(t+1)=x(t)-u(t),$ and revenue is derived by a random process $y(t+1)=w(t+1)$. <br><br>

A dynamic program can be formulated traditionally as 
$$V_t(x,y)=\underset{\mu\in \{0,1\}}{max} E\big[yu+V_{t+1}(x-u,w(t))\big]$$.<br>
However, with transformation above, the recursino can be reduced in observable-disturbance form as <br><br>
$$G_t(x)=E\big [\underset{\mu\in \{0,1\}}{max} \{w(t)u+G_{t+1}(x-u)\}\big].$$<br><br>

Note that $G_t(x)$ has similar interpretation as $V_t(x,y)$, namely, the optimal expected reward-to-go from time $t$ onward given state $x(t)$ at time $t$. Conceptually, we can consider recursion $G_t$ in a 2-stage manner as follows. First, state $x$ is realized but $y$ remains uncertain. We measure the optimal expected reward at this point, yielding $G_t(x)$. Then the value $y=w(t)$ is realized, and we make our optimal decision. This takes us to next state $x(t+1)$. 

$\mathbf{Exercise}$: A single-leg revenume managment problem.<br>
1. Assuming there are 10 classes. 
2. Demand $D_j$ is calculated through discretizing a truncated normal with mean 0 and standard deviation 2, on support $[0,20]$. Speciccally, take:
$$P(D_j = k) =\frac{\Phi((k + 0.5- 10)/2)-\Phi((k -0.5-10)/2)}{\Phi((20.5-10)/2)-\Phi((-0.5-10)/2)}, \quad k = 0,...,20$$
Note that this discretization and re-scaling verifies:
$$\overset{20}{\underset{k=0}{\Sigma}}P(Dj = k))= 1.$$
3. Total capacity available is C = 100.
4. Prices are $p_1 = 500; p_2 = 480; p_3 = 465; p_4 = 420; p_5 = 400; p_6 = 350; p_7 = 320; p_8 = 270; p_9 =
250$, and $p_{10} = 200$.<br><br>
Formulate the problem as a dynamic progrm to solve for optimal protection levels $y$ the total expected revenue $V_{10}(100).$



## Forecasting in revenue management

### Why is forecasting important in revenue management?

A revenue management system requires forecasts of quantities such as demand, price elasticity and cancellation probabilities. It is reported that 20% error reduction in forecasting leads to 1% revenue improvement. With new technology of collecting customer data in almost real time and advance of forecasting software packages, accurate forecasting adds significant values in revenue management. <br><br>

The forecasting module is a component of a revenue management system. It generates and updates forecasts for all product/fare combinations for all future dates. Generally, an initial forecast will be generated about one year prior to departure when the booking opens in most RM systems. Then the forecasts will be updated periodically as bookings and cnacellations are received over time. Typically, a forecast will be updated monthly when a flight is six months or more from departure and more frequently as departure approaches. Forecasts are typically updated daily for flights are within two weeks of departure. <br><br>

The forecast generated by RM systems are probablistic and they predict both a mean and standard deviation for future demand. As can be seen later, uncertainty plays a big role in updating booking limits.

### Forecasting process

Forecasting is a vast topic spanning a diverse range of fields including statistics,computer science, engineering and economics. Over many years, a core set of  forecasting methods have been developed and new improvements continue. Some of the forecasting methods are rigorous and others are largely heuristic in nature. <br><br>

Demand forecsting is more of an iterative process than techniques. As shown below, it starts with collecting and storing data. Actual modeling by statistical techniques is just an intermediate step in the overall process. More importantly, it is to monitor and manage the forecasting performance and update previous forecasts.<br><br>

<img src="C:/myPython/Fcst_Process.PNG" width="450" height="400">

### Forecasting methods
As can be seen above, the forecasting process starts with collecting and pre-processing relevant data and information. Now, we turn to forecasting methods, which explicitly use data to predict values of a sequence of data. In revenue management, we are mostly interested in forecasting demand,though sometimes we also need to estimate cancellation and no-show rates. <br><br>

<img src="C:/myPython/Fcst_Cost_Benefit.PNG" width="450" height="400">

In RM, the emphasis of forecasting methods is on speed, simplicity and robustness. We must balance accuracy with cost. The forecaster need to understand how accurate do I need to be for this product. Are incremental increases
in forecast accuracy worth the additional investment? It is also because of the balance and cost-benefit of forecasting that most forecasting algorithms in RM practice are variations of standard methods and most are not mathematically sophosticated. We first review standard forecasting methods and then further demonstrate enhanced forecasting techniques.<br><br>

Below is a quick summary of all forecasting methods. <br>
<img src="C:/myPython/Fcst_Models.PNG" width="450" height="400">

#### Classical Decomposition Approach

The steps of decomposition approach are shown below. It is also structural forecasting method.

1. Calculate seasonality of series
2. De-seasonalize raw data
3. Apply forecasting method
4. Re-seasonalize forecast

<img src="C:/myPython/Decomposition.PNG" width="450" height="400">

#### Exponential smothing methods

Exponential smoothing is an important family of forecasting techiniques. It originated as a data smoothing technique and later adapted to forecasting. Exponential smothing is another smoothing technique, similar to moving averages. The key difference is that the weights assigned to each period in history differ. For example, in 5 period moving average, each period weighted equally at 20% while in exponential smoothing, weights decrease exponentially with tim.<br><br>

It has 3 soothing Parameters
1. Level (Randomness) 鈥?Single ES Model
鈥?Assumes variation around a level<br>
鈥?$\alpha$<br>
2. Trend 鈥?Holt鈥檚 Model
鈥?Assumes linear trend<br>
鈥?$\beta$<br>
3. Seasonality 鈥?Winter鈥檚 Model
鈥?Assumes recurring pattern due to seasonal factors<br>
鈥?$\gamma$<br>

Below is a summary of the ESM family.

<img src="C:/myPython/ESM_Family.PNG" width="450" height="400">

#### Time-series methods

Box-Jenkins 鈥?ARIMA Modeling Process<br>
The process involves three basic stages:
1. Identify the tentative model.
2. Estimate the model鈥檚 parameters and testing.
3. Apply the model (forecasting).
If steps 2 and 3 do not meet expectations, then the process is
repeated and a new model is chosen and tested.

<img src="C:/myPython/Box_Jenkins.PNG" width="450" height="400">

#### Enhanced forecasting techniques

Most methods we have discussed so far need just history of data points to predict to future. However, it is important that the predicted time series is closely related to other data streams. Causal effect plays a big role in forecasting. 

##### Bayesian forecasting methods

Bayesian methods use Bayes rule to merge a prior belief about forecast values with information obtained from observed data. It is especially useful when there is no historial data such as new product launch. <br><br>

let $Z_1,Z_2,...$ be sequence of iid random variables. We assume $Z_t$ has density $f(z|\theta)$ where $\theta$ is a single unknown parameter. Since $\theta$ is unknown, we assume it is generated from a probablity density $g(\theta)$, which is in turn called the prior. It represents our current belief about the value of the parameter. Let $g_0(\theta)$ be out initial belief at $t=0$. When new data $z_1$ is observed, we may change our belief about the parameter $\theta$ as follows.

$$ g_1(\theta)=\frac{g_0(\theta)f(z_1|\theta)}{\int_{\theta} g_0(\theta)f(z_1|\theta)}$$

The Baues estimation of the parameter $\theta^*$ is then the expected value of $\theta$ based on the new posterior distribution as below.

$$\theta^*=\mathbf{E}(\theta)=\int_{\theta}\theta g_1(\theta)d\theta.$$

The it is used in forecasting as $\hat{Z_t}=\mathbf{E}[Z_t|\theta^*]$. Once new data $z_2$ is available, we repeat the procedure to get $g_2(\theta)$ and so on.

The challenge is to obtain the posterior distribution from a given prior. In certain cases,iIt turns out the posterior has same type of distribution as the prior. A pair of distributions having this property is said to be a conjugate family of prior distributions.  For example, $Z_t,t=1,2,...,N$ has a normal distribution with variance $\sigma^2$ and unknown mean $\mu$ which is $\theta$ discussed above. Further suppose $\mu$ has a normal distribution with mean $\eta$ and variance $\nu^2$. Then posterior of $\mu$ is also a normal distribution with mean

$$\frac{\sigma^2\eta+\nu^2\underset{k}{\Sigma} z_k}{\sigma^2+N\nu^2}$$
and varaince 

$$\frac{\sigma^2\nu^2}{\sigma^2+N\nu^2}$$.

## Chapter 1: Introduction to Revenue Management

### What is revenue management?

Every seller of a product or service faces a number of fundamental decisions. <br>

1. A child selling lemonade outside her house has to decide on which day to have her sale, how much to ask
for each cup, and when to drop the price (if at all) as the day rolls on.<br>
2. A homeowner selling a house must decide when to list it, what the asking price should be, which offer to accept, and when to lower the listing price鈥攁nd by how much鈥攊f no offers come in. <br>

Businesses face even more complex selling decisions. <br>
1. how can a firm segment buyers by providing different conditions and terms of trade that profitably exploit their
different buying behavior or willingness to pay?<br>
2. How can a firm design products to prevent cannibalization across segments and channels?<br>
3. Once it segments customers, what prices should it charge each segment?If the firm sells in different channels, should it use the same price in each channel?<br>
4. How should prices be adjusted over time, based on seasonal factors and the observed demand to date for each product?<br>
5. If a product is in short supply, to which segments and channels should it allocate the products?<br>
6. How should a firm manage the pricing and allocation decisions for products that are complements(seats on two connecting airline flights) or substitutes (different car categories for rentals)?<br><br>


 <font color=blue> Revenue management (RM) is concerned with such demand-management decisions1 and the methodology and systems required to make them. It involves managing the firm鈥檚 鈥渋nterface with the market,鈥?as it were鈥攚ith the objective of increasing revenues. RM can be thought of as the complement of supply chain management (SCM), which addresses the supply decisions and processes of a firm with the objective (typically) of lowering the cost of production and delivery.</font> 
 
### Demand-Management Decisions
 
 RM addresses three basic categories of demand-management decisions:<br><br>
1. Structural decisions: Which selling format to use (such as posted prices, negotiations, or auctions); which segmentation or differentiation mechanisms to use (if any); which terms of trade to offer (including volume discounts and cancellation or refund options); how to bundle products; and so on.<br>
2. Price decisions: How to set posted prices, individual-offer prices, and reserve prices (in auctions); how to price across product categories; how to price over time; how to mark down(discount) over the product lifetime; and so on.<br>
3. Quantity decisions: Whether to accept or reject an offer to buy; how to allocate output or capacity to different segments, products, or channels; when to withhold a product from the market and sale at later points in time; and so on.<br>

 Structural decisions about which mechanism to use for selling and how to segment and bundle products are normally strategic decisions taken relatively infrequently. Whether a firm uses quantity-based or price-based RM controls varies even across firms within a given industry.<br>
 
### What鈥檚 New About RM?
In one sense, RM is a very old idea. The theory of RM, at a broad level, is not new either.What is new about RM is not the demand-management decisions themselves, but rather how these decisions are made. The new approach is driven by scientific advances in economics, statistics, and operations research and at the same time the advances in information technology. <br>
The process of managing demand decisions with science and technology鈥攊mplemented
with disciplined processes and systems, and overseen by human analysts (a sort of 鈥渋ndustrialization鈥?of the entire demand-management process)鈥攄efines modern RM.

### The Origins of RM?
Where did RM come from? In short, the airline industry.<br>

The starting point for RM was the Airline Deregulation Act of 1978. With this act,the U.S. Civil Aviation Board (CAB) loosened control of airline prices, which had been strictly regulated based on standardized price and profitability targets.<br>

The potential of this market was embodied in the rapid rise of upstars such as PeopleExpress. A significant portion of price-sensitive discretionary travelers migrated to the new, low-cost carriers. For the majors, the price war with the upstarts was deemed almost suicidal. American solved these problems using a combination of purchase restrictions and capacity controll fares. American further embarked on the development of what became known as the Dynamic Inventory Allocation and Maintenance Optimizer system (DINAMO). These efforts on DINAMO represent,in many ways, the first large-scale RM system development in the industry. DINAMO was implemented in full in January 1985 along with a new fare program entitled Ultimate Super-Saver Fares, which matched or undercut the lowest discount fares available in every market American served.<br>

A large, modern airline today would just not be able to operate profitably without RM. By most estimates, the revenue gains from the use of RM systems are roughly comparable to many airlines鈥?total profitability in a good year (about 4% to 5% of revenues).<br>

### Industry Adopters Beyond the Airlines
The production-inflexibility characteristics of airlines are shared by many other service industries, such as hotels, cruise ship lines, car rental companies, theaters and sporting venues, and radio/TV broadcasters,to name a few. Indeed, RM is strongly associated with service industries.<br>

Retailers have recently begun to adopt RM, especially in the fashion apparel, consumer electronics, and toy sectors. Retail demand is highly volatile and uncertain, consumers鈥?valuations change rapidly over time, and with short selling seasons and long production and distribution lead times, supply is quite inflexible. On the technology front, the introduction of bar codes and point-of-sale (POS) technology has resulted in a high degree of automation of sales transactions for most major retailers.<br>

The energy sector has been a recent adopter of RM methods as well, principally in the area of managing the sale of pipeline capacity for gas transportation. Again, energy demands are volatile and uncertain, and the technology for generating and transmitting electricity and gas can be inflexible. Also, thanks to deregulation in the industry, there has been a lot of experimentation and innovation in the pricing practices of energy, gas, and transmission
markets.<br>

### A Conceptual Framework for RM
RM generally follows four steps:<br><br>
1. Data collection: collect and store relevant historical data such as prices, demand and causal factors.<br>
2. Estimation and forecasting: estimate the demand, price elasticity, cancellation rate, and so on.<br>
3. Optimization: find optimal control policies such as product allocations, prices, discounts and so on.<br>
4. Control: control inventory.<br><br>
In reality, the RM process involves cycling through the steps above in repeated intervals.<br><br>
Example: a quantity-based RM system<br>

<img src="C:/myPython/RMSystem.PNG" width="450" height="400">

## Chapter 2: Capacity Control with a Single Resourece
## <font color=blue> Static Models</font> 
Static Models Assumptions: 1) Single Resource; 2) Demand comes in a non-overlapping manner with inceasing reserve prices,i.e., in the sequece of $P_1>P_2>p_3>...$, that higher reserve price customers come earlier. 3) Demands are independent; 4) Demands are heterougenious; 5)Risk-neutral.
###  Single Resourece 2-class static model: Littlewoods Rule <br>
The littlewoods's rule was developed in 1970's. The practice was leading a decade ago with heurisitc algorithms in multi-class cases.<br><br>

$P_i, i=1,2$ are the rserve price of class $i$. Let $y_1^*$ be an optimal protection level of class 1. Formally, we have <br>

$$ P_2< p_1 P(D1>y_1^*)$$ and <br>
$$ P_2 \ge p_1 P(D1>y_1^*+1).$$
So optimal protection level $y_1^*$ is given by 
$$ y_1^*=F_1^{-1}(1-\frac{p_2}{p_1})$$

###  Connection of Littlewoods rule to Newsvendor model <br>
Consider a Newsvendor problem where we make a fixed decision $Q$, that is the protection level of the higher fare class of hotel rooms, then a random event $D$ with distribution $F$ occurs, the number of people requesting a room at the full fare. If we protect too many rooms, i.e., $D<Q$, then we end up earning nothing on $Q-D$ rooms. So the overage penalty $C$ is $r_L$ per unsold room. If we protect too few rooms, i.e., $D<Q$, then we forgo $r_H-r_L$ in potential revenue on each of the $D-Q$ rooms that could have been sold at the higher fare so the underage penalty $B$ is $r_H-r_L$. The critical ratio is<br><br>
$$\frac{B}{B+C}=\frac{r_H-r_L}{r_H}$$<br>
From the newsvendor analysis, the optimal protection level is the smallest value $Q^*$ such that<br><br>
$$F(Q^*)>\frac{B}{B+C}=\frac{r_H-r_L}{r_H}.$$

###  Single Resourece n-class static model: Geneal Case<br>
Seuqence of envets in a periods:<br><br>
1) Realizaion of $D_i$ in period $j$ <br>
2) Decision $u$ of quantity to accept of bookings where $u=u(j,x,D_j)$, and $x$ is the capacity at time $j$.<br>
3) Revenue $p_jU$ to be collected and proceed to next stage of $j-1$

Let $V_j(x)$ be the value function that represents the expected value at stage $j$ with capacity $x$. Hence the Belman euqaiton is <br><br>
$$V_j(x)=E[\underset{0\le u\le \min\{D_j,x\}}{Max} \{p_j u_j+V_{j-1}(x-u)\}]...(1)$$ <br>
with a boundary condition $V_0(x)=0$.<br>
#### Case 1: Demand and capcity are discrete<br>
Define $\Delta V_j(x)=V_j(x)-V_j(x-1)$ the expected marginal value of capacity at stage $j$. The Bellman equation $(1)$ can be re-written as <br><br>
$$V_{j+1}(x)=V_j(x)+E[\underset{0\le u \le min(D_j,x)}{Max}\{\Sigma_{z=1}^{u} \{p_{j+1}-\Delta V_j(x+1-z)\}]...(2)$$<br>
__Caveat__: Express out the terms in $\Sigma$ as follows to obtain the equation $(2)$ from $(1)$<br><br>
$$p_{j+1}-V_j(x)+V_j(x-1)$$
$$p_{j+1}-V_j(x-1)+V_j(x-2)$$
$$...$$
$$p_{j+1}-V_j(x+1-u)+V_j(x-u)$$<br>
The optimal control can be expressed in one of the following 3 ways. <br>
 1) Optimal protection levels $y_j^*=max\{x: p_{j+1}<\Delta V_j(x)\}, j=1,2,...,n-1.$ <br>
 2) Optimla booking limits $b_j^*=C-y_{j-1}^*$, where $j=2,3,...,n$ and $C$ is the full capacity.<br>
 3) Optimal bid prices $\pi_{j+1}(x)=\Delta V_j(x)$ and we accept a $z^{th}$ request if its price exceeds the corresponding bid price at stage $j+1$ as follows. 
$$
u^*(j+1,D_{j+1}) = \left\{
        \begin{array}{ll}
            0 & \quad p_{j+1}< \pi_{j+1}(x) \\
            max\{z:p_{j+1} \ge \pi_{j+1}(x-z)\} & \quad \text{Otherwise}
        \end{array}
    \right.
$$
#### Case 2: Demand and capcity are continuous<br>
Similar arguments follow as above with the same model $(1)$. The main differences are continuous variables $D_j,x,u$. The optimal protection levels can be defined by  <br>
$$y_j^*=max\{x:p_{j+1}< \frac{\partial{V_j(x)}}{ \partial{x}}\}$$
Further, we define $n-1$ fill events as follows. <br><br>
$$B_j(y,D)=\{D_1>y_1,D_1+D_2>y_2,...,D_1+D_2+...+D_j>y_j\}$$<br>
and we have a sufficient and necessary conditon for a vector of optimal protection levels as follows.<br><br>
$$P(B_j(y^*,D))=\frac{p_{j+1}}{p_1}$$
As can ben seen,the optimal protection levels $y_j$ are strictly increasing in $j$ if the revenues $p_j$ are strictly decreasing in $j$. In particular, littlewoods rule is a special case.<br>
### Single Resourece n-class static model: Heuristics<br><br>

#### Expected marginal seat revenue-version a (EMSR-a) <br>
The basic idea is to use littlewoods' rule of 2-class repeatedly. At stage $j+1$, the decision to make is the protection level $y_{j}$ for class $j$ and higher. Consider a single class $k$ among all remain classes $j,j-1,...,1$, we use reserve capacity $y_k^{j+1}$ for class $k$ and obtain <br><br>
$$p(D_k>y_k^{j+1})=\frac{p_{j+1}}{p_k}$$<br><br>
We repeat for all future classes $k=j,j-1,...,1$ and obtain <br><br>
$$y_j=\overset{j}{\underset{k=1}{\Sigma}}y_k^{j+1}$$
As can be seen, EMSR-a can be extremely conservative and produce protection levels that are larger than optimal in certain cases. This is because adding individual protection levels $y_k^{j+1}$ ingores pooling effect produced by aggregating demand across classes.\newline
#### Expected marginal seat revenue-version b (EMSR-b) <br>
This approximation is based upon aggregating demand rather than aggregating proection levels. Define aggregated future demand for classes $j,j-1,...,1$ by $$ S_j=\overset{j}{\underset{k=1}{\Sigma}}D_k,$$ and let the weighted average revenue be $$ \bar{p_j}=\frac{\Sigma_{k=1}^j p_kE[D_j]}{\Sigma_{k=1}^j E[D_j]}$$

### Example: 4 classes with iid normal demand as follows. <br>

$$D_1\sim N(17.3, 5.8)\quad \text{and}\quad P_1=1050$$
$$D_2\sim N(45.1, 15.0)\quad \text{and}\quad P_2=567$$
$$D_3\sim N(39.6, 13.2)\quad \text{and}\quad P_3=534$$
$$D_4\sim N(34.0, 11.3)\quad \text{and}\quad P_4=520$$

Solve for EMSR-a , EMSR-b and Optimal $y_j,j=3,2,1.$

Solution:<br>
1) Optimal protection levels<br>

$$P(D_1>y_1)=\frac{P_2}{P_1}$$
$$P(D_1>y_1,D_1+D_2>y_2)=\frac{P_3}{P_1}$$
$$P(D_1>y_1,D_1+D_2>y_2,D_1+D_2+D_3>y_3)=\frac{P_4}{P_1}$$

Solve for $y_1,y_2,y_3$.<br><br>

Reference code in R<br>

Mu=c(17.3,62.4)<br>
sigma=matrix(c(33.64,33.64,33.64,258.64),2,2)<br>
pmvnorm(lower = c(16.7,42.89),mean=Mu,sigma = sigma)<br>
qmvnorm(0.5086, mean=Mu,sigma = sigma, tail = "upper")<br><br>

Mu_3=c(17.3,62.4,102)<br>
sigma_3=matrix(c(33.64,33.64,33.64,33.64,258.64,258.64,33.64,258.64,432.88),3,3<br>)
pmvnorm(lower = c(16.7,42.8,72.3),mean=Mu_3,sigma = sigma_3)<br>
qmvnorm(0.4952, mean=Mu_3,sigma = sigma_3, tail = "upper")<br>

2) EMSR-a <br>
$$p(D_3>y_3^4)=\frac{p_4}{p_3}\Rightarrow y_3^4=39.6+\Phi^{-1}(\frac{p_3-p_4}{p_3})*13.2$$<br>
$$p(D_2>y_2^4)=\frac{p_4}{p_2}\Rightarrow y_2^4=45.1+\Phi^{-1}(\frac{p_2-p_4}{p_2})*15.0$$<br>
$$p(D_1>y_1^4)=\frac{p_4}{p_1}\Rightarrow y_1^4=17.3+\Phi^{-1}(\frac{p_1-p_4}{p_1})*5.8$$<br>
We further obtain $y_3=y_3^4+y_2^4+y_1^4\dot{=}14.1+24.2+17.4=55.7$<br><br>

2) EMSR-b <br>
At stage 4, the aggregated demand and weight-average revenue have the forms as follows. Since $D_j, j=1,2,3$ are $i.i.d$ normally distributed we have
$$S_4=D_3+D_2+D_1\sim N(102,432.88),$$<br>
and $$\bar{p_4}=\frac{1050*17.3+567*45.1+534*39.6}{102}=636.11 .$$
As a result, we obtain $y_4=102+20.81*\Phi^{-1}(1-\frac{520}{636.11})\dot{=}83.0$

## <font color=blue> Dynamic Models</font> <br>
We relax the assumption of demand for classes arrives in a strict mannger of increasing revenues. Instead we allow for arbitrary order of arrivals and further assume poisson arrivals to make it tractable. However, we maintain the assumption of independent and heterogeneous demand. <br><br>
As demand comes in arbitrart classes, there is no one-to-one relationshi between period and class. We denote $t$ for periods and $j$ for classes. By a sufficiently fine discretization of time periods, we assume at most one arrival occurs in each period and further denote $\lambda_j(t)$. We also have $$\overset{m}{\underset{j=1}{\Sigma}} \lambda_j(t)\le 1.$$

The Bellman equation has the following form.
$$ V_t(x)=E[\underset{u \in \{0,1\}}{max}\{R(t)u+V_{t+1}(x-u)\}]$$ <br>
$$=V_{t+1}(x)+E[\underset{u \in \{0,1\}}{max}\{R(t)-\Delta V_{t+1}(x)\}u]$$ where $\Delta V_{t+1}(x)$ is the expected marginal value. The bounday conditions are  $V_{T+1}(x)=0$, $T$ is the total # periods and $V_t(0)=0$.
The optimal control can be expressed in the follwoing 3 ways.

1). Bid prices equal the marginal values as $\pi_t(x)=\Delta V_t(x)$<br>
2). Optimal protection levels $y_j^*(t)$ satisfy $y_j^*(t)=max\{x:p_{j+1}<\Delta V_{t+1}(x)\}, j=1,2,...,n-1.$<br>
3). Optimal booking limits define as $b_j^*(t)=C-y_{j-1}^* (t)$, $j=2,...,n.$

## <font color=blue> Customer Choice Models</font> <br>

The key assumption in models described above is indenpendent and heterogeneous demand that are independent of capaciy availability and other classes. However, in reality the customer's behavior depnds on whether discount fare is available. Buy-up and diversion are both likely. In this section, we model the buy-up effect in a standard 2-class setting. <br><br>

Recall littlewoods' rule of accpeting class 2 request iff $p_2\ge p_1P(D_1>x).$ Now we further suppose there is a probaaility $q$ tha a customer for class 2 will buy class 1 if class is closed. Hence, it is optimal to accept class 2 if $$ p_2\ge (1-q)p_1P(D_1>x)+qp_1.$$

The first part of right hand side above represents the expected value of class 2 customer doesn't buy up when class 2 is closed upon request. At the same time, the second part represents expected value of buying-up in the similar situation for him\her. We further notice that full right hand side above is strictly larger than that in littlewoods' rule. It is more likely that class 2 will be rejected in buy-up scenarios. As a broader application, the same approach can be used in EMSR-a and EMSR-b where 2 classes are itereratively compared and buy-up factor can be incorpporated.

## Chapter 3: Network Control

Network control problems deal with quantitiy-based product requests where each product in this case called ODIF origin-destination itinerary fare calss combination consumes multiple resources. <br><br>
Types of controls: <br><br>
1. Parititioned booking limits <br>
It allocates a fixed amount of capacity on each resource fo every productthat is offered. They are non-overlapping or partitioned. Theorectically, they are used to provide bounds on the optimla network revenue.<br><br>
2. Vitrual nesting control<br>
It is a hybrid of network and single-resource controls. It uses single-resource nested-allocation controls for each resourece in the network that requires virtual classes. The process is called indexing which groups together sets of products that use a given set of resource. Its main benefits is to be able to preserve the single-resource control structure. <br><br>
3. Bid-price control<br>
It is a simple extensin of single-resource bid-price in network setting. The bid price of a network product is summatin of bid prices of resources used. The bid price is normally interpreted as an estimate of the marginal cost to the network of consuming the next incremental unit of the resource's capacity. <br><br>

## <font color=blue> Theory of optimal network controls </font> 
Notation: <br>
m resources, n products, incidence matrix $A=[a_{ij}]$, where $a_{ij}=1$ if resource $i$ is used by product $j$.$A_{j}$ is incidence vector for product $j$.<br><br>
The state of network is denoted by $x=(x_1,x_2,...,x_m)$ and if product $j$ is sold, the state of the network changes to $x-A_j$. There are totally $T$ periods and we assume taht there is at most one request for a product in each period by partiicitionaing times fine enough.<br><br>
Demand in period $t$ is modeled as $P(t)=(p_1(t),p_2(t),...,p_n(t))$. If $p_j(t)=p_j>0$, this indicates request for product $j$ occurred and associated with price $p_j$. We also assume $P(t),t\ge 1$ is independent over time $t$.<br><br>
Decisions to make are the $n$-vector $u(t)$, wehre $u_j(t)=1$ if we accept a request for product $j$ in period $t$. It is further a function of remaining capacity vector $x$ and price $p_j$ of product $j$ so we write $u_j(t)=u_j(t,x,p_j)$. The constraints apply as $\mathbb{u}(x)=\{u\in \{0,1\}^n:Au\le x\}.$<br>

###  Structure of optimal controls <br> <br>

Value functin above can be wriiten as the follwing Bellman equation. <br><br>
$$V_t(x)=E[\underset{u \in \mathbb{u}(x)}{max}P(t)^{T}u(t,x,p)+V_{t+1}(x-Au)]$$
with boundary conditon $V_{T+1}=0 \forall x.$ An optimal solution satisfiles <br>
$$u_j^*(t,x,p_j)= \left\{
        \begin{array}{ll}
            1 & \quad if\quad (p_j)\ge V_{t+1}(x)-V_{t+1}(x-A_j) \quad\text{and}\quad A_j\le x \\
            0 & \quad \text{Otherwise}
        \end{array}
    \right.$$
     It says that the optimal policy is to accept a request for product $j$ at price $p_j$ if and only if the capacity is enough and the prie exceeds the marginal opportunity cost.<br><br>

###  Bid price controls <br> <br>
We suppose the value function has a gradient $\Delta V_{t+1}(x)$. The optimal control can be approximated by the folllowign bid prices.<br> 
$$P_j\ge V_{t+1}(x)-V_{t+1}(x-A_j)$$<br>
$$\dot{=} \Delta V_{t+1}^T(x)A_j$$<br>
$$= \underset{i\in A_j}{\Sigma} \pi_i(t,x),$$
where $\pi_i(t,x)=\frac{\partial{V_{t+1}(x)}}{\partial{x_i}}.$ The bid price control policy specifies a set of bid prices for each resource, at each point in time and for each capacity level such that we accpet a request for a particular product if and only if there is available capacity and the price exceeds the sum of bid prices for all the resources used by the product.<br><br>

Despite the generality and simple extension of bid prices from single resource to network, bid prices are notalways optimal form of control as the example below shows.<br><br>
Example: Consider a network with 2 resources. There is one unit of capacity of each resource and two time periods. The data are shown as below.<br>

\begin{array} {|r|r|} \hline 
Period & Product & A_j & Fare & Probability \\ \hline
1 &1 & (1,0) &$250 &0.3 \\
  &2 & (0,1) &$250 &0.3 \\ 
 &3 & (1,1) &$500 &0.4 \\ 
2  &3 & (1,1) &$500 &0.8 \\
 &NA & &  & 0.2 \\ \hline
\end{array}
Questions: 1) what is a bid price policy? 2) what does best bid price control look like? 3) how is an optimal control policy?<br>
Hint to optimal policy <br>

\begin{array} {|r|r|} \hline 
Product in period (1,2)&  Probability & Revenue\\ \hline
 (1,3)  &0.24 & $500\\
 (2,3)  &0.24 & $500\\ 
(3,3)  &0.32 & $500\\ 
(1,0)  &0.06 & $0\\
(2,0)  &0.06 & $0\\
 (3,0)  &0.08 & $500\\ \hline
\end{array}
The derived optimal expected revenue is $440=0.88*500.$<br>

###  Virtual nesting controls <br> <br>

Virtual Nesting starts by assigning every origin-destination fare(ODF) to a bucket in a resource that is used in the ODF.

1. A bucket works like a fare class.
2. A bucket is a collection of ODF鈥檚.
3. Think of higher buckets as higher customer fare classes where we price the resources higher. <br>

ODF-to-bucket assignment is called indexing. Given this assignment, find the booking limits of an ODF by using EMSR heuristics or another method. Virtual Nesting is attributed to American Airlines and developed in 1983. The key issue here is indexing.

## <font color=blue> Approximation in network controls </font> 
For any network of realistic size, computing the value function $V_t(x)$ exactly is essentially hopeless. Approximatin to optimal control policies provides most useful results in practic, particularly, the estimates on the displacement cost or opportunity cost. Suppose an approximation method M that has approximation to value function as $V_t(x)^M(x)$. We can estimate the displacement cost as follows. <br>

$$V_t^M(x)-V_t^M(x-A_j)\approx \Delta V_t^M(x)A_j$$<br>
where $\Delta V_t^M(x)$ is the gradient of the value function approximation $V_t(x)^M(x)$ assuming the gradient exists. Then the bid price are defined as <br>
$$\pi_i^M(t,x)=\frac{\partial V_t^M(x)}{\partial x_i}.$$<br>
If the gradient doesn't exist, then $\Delta V_t^M(x)$ is typically replaced by a subgradient. If the approximation is discrete, then first differences are used in place of the partial derivatives.

### Deterministic linear programming <br>
Let the aggregate demand at time t for product $j$ be denoted by $D_j$ with mean $\mu_j$.Further $\mathbb D=(D_1,D_2,...,D_n)$ and $\mathbb \mu=\mathbb E [\mathbb D]$. The deterministic Linear Programming(DLP) Model can be expressed as follows.<br><br>

\begin{array}
&V_t^{DLP}(x)=&  max \quad P^Ty
&s.t. \quad Ay\le x
&\quad 0\le y \le \mu
\end{array}<br>
The decision variables $y=(y_1,y_2,...,y_n)$ represent the partitioned allocation of capacity for each of the $n$ products. This approximation treats demand as it is deterministic and equal to its mean $\mu$. Using Jensen's equality, one can show $V_t^{DLP}(x)$ is in fact an upper bound on the optimal value function. More often, the primal allocations are discarded due to poor revenue performance. However, since solving DLP can be very efficiently, the dual prices $\pi^{DLP}$ are used as bid prices.Empirical studies show that the performance of frequently updated dual prices is respectable.<br><br>
Example: An airline network with 10 city pairs as shown below.<br>
<img src="C:/myPython/AirNet.PNG">
Solve for a deterministic solution assuming demand

### Virtual nesting <br>

Example: A simple network with single class as shown below.<br>
<img src="C:/myPython/AirNet2.PNG">
Solve for a virtual nesting control.

## Chapter 8: Pricing theory




```python

```
