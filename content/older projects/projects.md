---
title: Projects
full_title: Past Projects
weight: 1
---


A selected list of past and current projects.

### Police Early Intervention System
[project webpage](https://dssg.uchicago.edu/project/expanding-our-early-intervention-system-for-adverse-police-interactions/) | [project github repo](https://github.com/dssg/police-eis/) 

Adverse interactions between police and the communities that they are tasked with protecting are an ongoing problem in the United States. The worst of these interactions have fatal consequences, but even interactions that don't result in death do irreparable harm and are devastating to the citizens involved. Preventing these interactions is critical to a just society and is one step in building trust between communities and police.

During the summer of 2016, I was a data science fellow with [Data Science for Social Good](https://dssg.uchicago.edu/). I worked on a team that developed an early intervention system in partnership with the Metropolitan Nashville Police Department. This system is designed to identify police officers who are at high risk of having an adverse incident; so that the department can step in and provide additional training, resources, counseling, or take other appropriate actions in order to try and prevent adverse incidents from happening in the first place. Although it would be impossible to predict and prevent all negative interactions between police and the public, an early intervention system is one piece of a broader movement for criminal justice reform that can help lead to fewer negative interactions and better outcomes for the communities that the police serve.

In addition to developing a predictive model for our partner department, we also worked closely with [another team](https://dssg.uchicago.edu/project/building-a-deeper-police-early-intervention-system/) who was working with the Charlotte Mecklenburg Police department. Together we developed a pipeline, database schema, and model that is department-independent. This added layer of collaboration is a key proving ground that the systems we developed can be implemented not just at one department, but, given the right data, almost any department in the country.

We used 5 years of internal department data (including arrest records, dispatches, patrol areas, internal and external discipline, citizen complaints, &c.) as inputs to our model. For each officer, we made a prediction (which can also be thought of as a risk score) of how at risk of being involved in an adverse incident that officer is over the next year. Our best performing model (a variation on random forests) correctly identified 80% of officers who went on to have an adverse incident (during our test period), while only requiring intervention on 30% of officers in the department. This is a drastic improvement over using the current state of the art in most police departments (a threshold-based flagging system): which would have needed to intervene on 67% of the department for the same level of accuracy.

Since the summer, the [Center for Data Science and Public Policy](http://dsapp.uchicago.edu/) has continued work with both police departments and is in the process of implementing these models. This is the first data-driven early intervention system of its kind to be implemented in any department in the United States.