# Errors in dataset of 107 used for MODELS Submission

This page offers a complete overview of the 12 errors supported by the tool.

## E1: The opposite of a transient reference must be transient if it is proxy resolving

This error is triggered when a transient reference has an opposite that is not reference declared as transient. This error appears in the dataset only twice and in the same model. As can be seen, the transient reference children (left) has the opposite parent in class Control that is set as not transient (right). The multiple resolutions in this case are related to changing children to non-transient or parent as transient.
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E1.png?raw=true)

## E2: The opposite must be a feature of the reference's type 
Error E2 appears in the dataset only once in a model called activityDiagram.ecore. This is related to the fact that a reference, in this case elements in the class *Activity* has set the opposite as *activity* in class *Element*, that seems to be empty. This reference in fact has been erroneously declared in class *ControlFlow*. 
The resolution may be multiple, as for instance removing the reference, or setting another reference as opposite in the right class, or even move the reference set as opposite from the wrong class to the correct one. 
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E2.png?raw=true)

## E3: The opposite of the opposite may not be a reference different from this one 
In Fig.~\ref{fig:E3*, E3 is shown, where for the reference *deployed* is set as opposite the reference *deployed*, but not the opposite. 
 Indeed the diagram of the ecore model shows two references instead of a single one, since in one reference the opposite is unset. For this reason the errors says that an opposite r2 of a reference r1 must be set with the same type of r1. In this case it is not declared with a different type but it is unset. The possible solutions for this error could be to set the type of r2 to the type of r1, assigning a new type to both references or remove r2.
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E3.png?raw=true)

## E4: Not transient Attribute so it must have a data type that is serializable
Error E4 appears 7 times in the dataset and it reports that an attribute declared as transient must have a datatype that serializable. An example of a models containing E4 is reported in Fig.~\ref{fig:E4*. In this case the attribute *domainResource* is declared as transient, but its type *EResource* is not serializable. The resolution can be based on two options: either make it not transient, set it to a different type, or make the datatype serializable. 
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E4.png?raw=true)

## E5: A primitive type cannot be used in this context
This error exposes "The primitive used type cannot be used in this context" and appears in 4 cases in the repository in the same domain model, i.e. *OPF31.ecore*. In particular the set datatype for the attribute *coordinatePairs* is a Map of EFloat. EFloat cannot be used in this context and for this reason we would need to replace it with another type. There might be many possibilities to type the attribute and hence multiple potential solutions. 
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E5.png?raw=true)

## E6: Two or more Classifier with the name name
Two or more classifiers with the same name cause error E6, present twice in the dataset. Specifically the model car.ecore contains two class with same name but different letter casing. Precisely  *AirCond* and *Aircond* inheriting from the same classifiers can be seen in Fig.~\ref{fig:E6*. This lead to the hypotesis that the modeler didn't check the model and added the same class twice during the development process. The multiple resolutions for this error include renaming or removing any of the classifiers.
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E6.png?raw=true)

## E7: Two or more feature with the same name
The analyzed repository reports this error 20 times in multiple models. This error is identified when two or more feature in the same classifier have been defined with same name. 
The error is also triggered when the modeler defines two features with same name but different letter casing, as we show in Fig.~\ref{fig:E7*. In *gsml.ecore* the model contains a class *Course* where two features have been defined, i.e. *gradingscheme* and *gradingScheme*. We may think that this error comes from a mistake of the modeler, that created a composition relation and an association with same name.  This error is at the warning level as can be seen from the icon on the class *Course* and can be repaired in different ways, including renaming, removing or moving any of the faulty features.
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E7.png?raw=true)
## E8: Invalid specified literal 
 Error E8 "Invalid specified literal" is quite diffused in the analyzed dataset, 166 times. In particular this error 
This error basically in a warning saying that the default value specified is not coherent with the literals specified in the enumeration. Indeed in this case the default value specified for the attribute *limitType* is 1, when the literals on the enueration, set as datatype, are the following: Reporting, Hard, SoftLinear, SoftQuadratic. Maybe the developer wanted to specificy *Hard* as default value, being at the position 1 of the possible literals. 
Possible solutions are to modify the literal value in the attribute with any of the possible literals, modify the default in the datatype enumeration, etc.
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E8.png?raw=true)

## E9: Not well formed name 
Not well formed name is another error diffused in the repository, even if most of the occurrences are in the model *GUIdancerComponentHierarchy.ecore*. In Fig.~\ref{fig:E9* we reported an excerpt of this model, where two of the classes have not well formed names. Indeed the classes contain forbidden characters, e.g., / or empty spaces in class name. 
To resolve this issue we could trim and remove the unexpected characters, split the class name with the forbidden char and take the first or the last part, etc. 
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E9.png?raw=true)

## E10: Operation with the same signature as an accessor method
E10 reports that an operation cannot be declared with same signature as an accessor method for a feature. This is the case of *signature.ecore* where, as can be seen in Fig.~\ref{fig:E10*, the modeler has declared an operation *getFunction()* with return type String, but there is also a co-existing feature *function* of type String in the same class. This will be in conflict with the automatically generated method by EMF for the feature, since EMF API will generate getters and setters for the structural features of the classes.
 Possible resolutions include modifying the signature for either the operation or the feature.
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E10.png?raw=true)

## E11: A containment or bidirectional reference must be unique if its upper bound is different 
This error is one of the most diffused and it is about setting a unique containment reference if the upper bound is different from 1. In this model reported in Fig.~\ref{fig:E11*, the containment reference *xMLNSPrefixMap* and *xSISchemaLocation* are not declared as unique, but its upperBound is set to -1, violating this uniqueness constraint of a containment relationship. For this reason, the possible resolutions are various, e.g., set the upperbound to 1, set the unique property, delete the faulty reference or unset the containment. 
This error is quite diffused since 160 occurrences have been matched in the dataset. 
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E11.png?raw=true)
## E12: A containment reference of a type with a container feature that requires instances to be contained elsewhere cannot be populated
Last discussed error is E12, namely ``A containment reference of a type with a container feature that requires instances to be contained elsewhere cannot be populated''. 
 This error seems to be very diffused in the dataset, since it is also quite difficult to be understood, especially if the model is big. 
 In fact, as can be seen from Fig.~\ref{fig:E12*, reference *childNodes* is a containment reference of type *ChildNode*, but in the same class also another contained reference is set, namely *nodes*. 
 For this reason the modeler has to understand which one of the relationship is right and set correctly the containment. 
 Multiple resolutions hence include setting one of the parts in the relationship as containment and removing in the other one, but also modifying any reference direction or even removing in case of duplicates.
![enter image description here](https://github.com/models2020modelsrepair/ModelsRepair/blob/master/E12.png?raw=true)
