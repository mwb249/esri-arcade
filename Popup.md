### "Join" a non-spatial table to a feature layer
Useful for joining table attributes to features in another layer.

```javascript
// Create variables for the non-spatial table and tax parcel PIN
var tbl = FeatureSetByName($map, "Tax Parcel Attribute");
var f_pin = $feature.PIN;

// Construct a SQL expression
var sql = "PIN = '" + f_pin + "'";

// Outputs messages (useful for debugging)
Console(sql);

// Run SQL query against the non-spatial table 
var records = Filter(tbl,sql);

// Get total record count, instinate empty variable for return
var total_records = Count(records);
var restriction = "";

// Update the return variable with first record or "None"
if (total_records > 0) {
    var first_record = first(records);
    var restriction = first_record.BURNPERMITRESTRICTION;
} else {
    var restriction = "None";
}

return restriction;
```

### GeoEnrich layer with attributes from intersecting features in another layer

```javascript
var fs_all = FeatureSetByName($map,"MABAS Box Card Areas");
var fs_fire = Filter(fs_all, "BOXALARMTYPE LIKE 'FIRE'");
var fs_intersect = Intersects(fs_fire, Centroid($feature));
var boxcard = First(fs_intersect);
var boxcard_number = boxcard.BOXALARMNUMBER;
return boxcard_number;
```

### Construct a dynamic URL (BS&A example)

```javascript
var urlsource = 'https://bsaonline.com/SiteSearch/SiteSearchResults?SearchCategory=Parcel+Number&';
var pin = $feature.CVTTAXCODE + $feature.PIN;
var cvt_id = "";

if ($feature.CVTTAXCODE == /*Independence Twp*/ "J ") {
    cvt_id = "268";
} else if ($feature.CVTTAXCODE == /*Rochester Hills*/ "70") {
    cvt_id = "385";
} else if ($feature.CVTTAXCODE == /*City of Rochester*/ "68") {
    cvt_id = "1655";
} else if ($feature.CVTTAXCODE == /*Orion Twp*/ "O ") {
    cvt_id = "1637";
} else {
    cvt_id = "";
}

var params = {
  SearchOrigin: '0',
  SearchText: pin,
  uid: cvt_id
};

return urlsource  + UrlEncode(params);
```
