```python
%%html
<!--Script block to left align Markdown Tables-->
<style>
  table {margin-left: 0 !important;}
</style>
```


<!--Script block to left align Markdown Tables-->
<style>
  table {margin-left: 0 !important;}
</style>



# ENGR 1330 – Computational Thinking and Data Science Fall 2020

## Concrete Strength Predictor Final Project - Background

The Compressive Strength of Concrete determines the quality of Concrete. 
The strength is determined by a standard crushing test on a concrete cylinder, that requires engineers to build small concrete cylinders with different combinations of raw materials and test these cylinders for strength variations with a change in each raw material. 
The recommended wait time for testing the cylinder is 28 days to ensure correct results, although there are formulas for making estimates from shorter cure times.
The formal 28-day approach consumes a lot of time and labor to prepare different prototypes and test them; the method itself is error prone and mistakes can cause the wait time to drastically increase.

One way of reducing the wait time and reducing the number of combinations to try is to make use of digital simulations, where we can provide information to the computer about what we know and the computer tries different combinations to predict the compressive strength.
This approach can reduce the number of combinations we can try physically and reduce the total amount of time for experimentation. 
But, to design such software we have to know the relations between all the raw materials and how one material affects the strength. 
It is possible to derive mathematical equations and run simulations based on these equations, but we cannot expect the relations to be same in real-world. 
Also, these tests have been performed for many numbers of times now and we have enough real-world data that can be used for predictive modelling.


## Objective(s):
- Literature scan on concrete design, and utility of a predictive approach
- Analyse an existing concrete compressive strength database and build a data model to predict the compressive strength of a concrete mixture.
- Build an interface to allow users to enter concrete mixtures and return an estimated strength and an assessment of the uncertainty in the estimate
- Build an interface to allow users to add observations to the underlying database, and automatically update the Data Model to incorporate the new observations

## Tasks: 

**Literature Research:**
- Describe the challenge of concrete mixture design and the importance of compressive strength.
- Summarize the value of a data model in the context of the conventional approach to strength prediction

Some places to start are:
- I-Cheng Yeh, “ Modeling of strength of high performance concrete using artificial neural networks,” Cement and Concrete Research, Vol. 28, №12, pp. 1797–1808 (1998). https://archive.ics.uci.edu/ml/datasets/Concrete+Compressive+Strength

- Laskar, Aminul Islam. (2011). Mix design of high-performance concrete. Materials Research, 14(4), 429-433. Epub November 21, 2011.https://doi.org/10.1590/S1516-14392011005000088 or http://54.243.252.9/engr-1330-psuedo-course/CECE-1330-PsuedoCourse/6-Projects/P-ConcreteStrength/Mix_Design_of_High-performance_Concrete.pdf

-  Ahsanul Kabir, Md Monjurul Hasan, Khasro Miah, “ Strength Prediction Model for Concrete”, ACEE Int. J. on Civil and Environmental Engineering, Vol. 2, №1, Aug 2013.

- https://towardsdatascience.com/concrete-compressive-strength-prediction-using-machine-learning-4a531b3c43f3

- Castro, A.L. & Liborio, J.B.L. & Valenzuela, Federico & Pandolfelli, Victor. (2008). The application of rheological concepts on the evaluation of high-performance concrete workability. American Concrete Institute, ACI Special Publication. 119-131.  copy at: http://54.243.252.9/engr-1330-psuedo-course/CECE-1330-PsuedoCourse/6-Projects/P-ConcreteStrength/ArtigoHPC026_CASTROetalfinal.pdf

- de Larrard, François & Sedran, Thierry. (2002). Mixture-proportioning of high-performance concrete. Cement and Concrete Research. 32. 1699-1704. 10.1016/S0008-8846(02)00861-X. copy at: http://54.243.252.9/engr-1330-psuedo-course/CECE-1330-PsuedoCourse/6-Projects/P-ConcreteStrength/Mixture-ProportioningCCR-deLarrardSedran-full.pdf

**Database Acquisition**
- Get the database from the repository: https://archive.ics.uci.edu/ml/machine-learning-databases/concrete/compressive/Concrete_Data.xls
- Supply links to any additional databases discovered during the literature research
- A copy of the database is located at: http://54.243.252.9/engr-1330-psuedo-course/CECE-1330-PsuedoCourse/6-Projects/P-ConcreteStrength/concreteData.xls If you cannot access the original database you can use this copy

**Exploratory Data Analysis**
- Describe (in words) the database.
- Reformat as needed (column headings perhaps) the database for subsequent analysis.
- Select possible data model structures (multi-feature linear model, power-law, ...)
- Select possible data model "fitting" tools (ordinary least squares,lasso regression, decision trees, random forests, ...)

**Model Building**
- Build data models
- Assess data model quality (decide which model is best) 
- Build the input data interface for using the "best" model
- Using your best model determine projected concrete strength for 5 possible mixtures in the table below:

|Cement|BlastFurnaceSlag|FlyAsh |CoarseAggregate|FineAggregate|Water|Superplasticizer|Age|
|:---|:---|:---|:---|:---|:---|:---|:---|
|175.0|13.0|172.0|1000.0|856.0|156.0|4.0|3.0|
|320.0|0.0|0.0|970.0|850.0|192.0|0.0|7.0|
|320.0|0.0|126.0|860.0|856.0|209.0|5.70|28.0|
|320.0|73.0|54.0|972.0|773.0|181.0|6.0|45.0|     
|530.0|359.0|200.0|1145.0|992.0|247.0|32.0|365.0|                
       
**Documentation**
- Training video on how to use your tool, and demonstrate the tool(s) as they are run
- Project management video 
- Interim report (see deliverables below); this document must be rendered as a .pdf, but you are free to use your favorite writing software (Word,LibreOffice, ...).
- Final Report (see deliverables below)

## Deliverables:

#### Part 1 (due November 24):
A report that briefly describes the concrete strength database and how you plan to solve the tasks of creating a suitable data model.  
- Break down each task into manageable subtasks and describe how you intend to solve the subtasks and how you will test each task. (Perhaps make a simple Gantt Chart)
- Address the responsibilities of each team member for tasks completed and tasks to be completed until the end of the semester. (Perhaps make explicit subtask assignments)

Your report should be limited to 4 pages, 12 pt font size, double linespacing (exclusive of references which are NOT included in the page count).  You need to cite/reference all sources you used.  

#### Part 2 (due on Final Exam day):
- A well-documented JupyterLab (using a python kernel) analysis and implementation for the data model.
- A well-documented JupyterLab (using a python kernel) implementation for the data model user interface.
- A well-documented JupyterLab (using a python kernel) implementation for the database update interface.

**Above items can reside in a single notebook; but clearly identify sections that perform different tasks.**

- A how-to video demonstrating performance and description of problems that you were not able to solve.
- A project management video (up to 5 minutes) in which you explain how you completed the project and how you worked as a team.

**Above items can reside in a single video; but structure the video into the two parts; use an obvious transition when moving from "how to ..." into the project management portion.**  Keep the total video length to less than 10 minutes; submit as an *unlisted* YouTube video, and just supply the link (someone on each team is likely to have a YouTube creator account).  Keep in mind a 10 minute video can approach 100MB file size before compression, so it won't upload to Blackboard and cannot be emailed.


```python

```
