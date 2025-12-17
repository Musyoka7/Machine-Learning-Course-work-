Dear all,

A question has come up about how Tasks 2, 3 and 5(a) are intended to be completed. Though I explained it in the lab session(s), I would again clarify this for everyone so you can align your implementations and reports with the intended design of the coursework.

1. What is expected in Task 2 (and Task 3)?
For Task 2, you should treat each three-digit combination (e.g. 037, 591, …) as a single class.

There are 1000 possible three-digit combinations: 000–999.

Each image therefore has one label out of 1000.

Both of your Task 2 models:

the logistic regression or Decision Tree, and

the CNN baseline, should be set up as 1000-way single-label classification models.

In other words, for Task 2 the model does not explicitly know that the label is “three digits”; it just sees one out of 1000 class IDs. Task 3 then builds on your best Task 2 model (usually the CNN) and looks at improving it (e.g. with regularisation, augmentation, or architectural changes), still in this 1000-class setting.

2. What is different about Task 5(a)?
Task 5(a) is not asking you to repeat Task 2. It is intentionally more ambitious and asks you to use the structure of the label more intelligently.

The brief for Task 5(a) is:

“analyse the multi-label structure of the problem and identify and implement an alternative CNN model … without requiring you to split the image first.”

There are two key parts to this:

(a) Analyse the “multi-label” structure
Here, we want you to think carefully about the nature of the target:

Each image contains three ordered digits.

You can think of the label for each image as three separate digits:

a first digit (digit_1)

a second digit (digit_2)

a third digit (digit_3)

Each of these digits can be any number from 0 to 9, and together they form the three-digit answer for that image.

This is richer than just saying “the label is one number between 0 and 999.” There is internal structure you could choose to model.

In your report, you should therefore discuss and compare:

Treating the triple as a single 1000-way class (the Task 2 baseline), versus

Treating it as a structured, multi-output label (three digits predicted together, as in Task 5(a)).

You should also comment on why using this structure might help, for example:

Sharing features for all three positions via a common CNN backbone.

Letting the network specialise different output “heads” for each digit position.

Potentially improving generalisation to unseen combinations of digits.

(b) Design an alternative CNN that uses this structure
Task 5(a) then asks you to propose and implement a CNN that explicitly uses the “three digits” idea, but:

without physically splitting the image into three crops (that is what Task 4 explores), and

in a way that is clearly different in spirit from the simple 1000-way classifier in Task 2.

Conceptually, for example (this is just to guide your thinking, not a required design):

A shared CNN that processes the full 84×84 image to extract features.

Then multiple outputs (or “heads”) that each predict one digit (first, second, third) based on those shared features.

The expectation in Task 5(a) is that you:

Use this more structured design to respect the three-digit nature of the label, and

Show that it can perform better than your Task 2 CNN, and ideally be similar to or competitive with your “split image” approach from Task 4.

I hope this clarifies the intended distinction between Tasks 2/3 and Task 5(a). Please refer to this announcement when finalising your implementations and reports.

Best wishes,