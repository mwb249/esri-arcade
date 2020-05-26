### Address Labels

Split combined address (number & name) field into an array. Return the address number.
```javascript
var address_array =  Split($feature.SITEADDRESS, ' ', 1, 'true');
return address_array[0]
```

When using stacked parcels (many related records, condos, etc), only display address numbers for the "keypin" parcel.
This expression also splits a combined address field into an array.
```javascript
var address_array =  Split($feature.SITEADDRESS, ' ', 1, 'true');
When($feature.PIN ==$feature.KEYPIN, address_array[0], None)
```
