### Visualize features based on their age:

```javascript
var inst_date = $feature.INSTALL_DATE;
var age = DateDiff(Now(), inst_date, "years");
var age_class = "";

if (age > 50) {
    age_class = "Over 50 years";
} else if (age > 40) {
    age_class = "Between 40 and 50 years";
} else if (age > 30) {
    age_class = "Between 30 and 40 years";
} else if (age > 20) {
    age_class = "Between 20 and 30 years";
} else if (age > 10) {
    age_class = "Between 10 and 20 years";
} else if (age > 5) {
    age_class = "Between 5 and 10 years";
} else {
    age_class = "Less than 5 years";
}

return age_class;

```
