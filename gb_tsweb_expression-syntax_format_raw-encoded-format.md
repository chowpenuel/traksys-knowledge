# Raw/Encoded Format

When dealing with URLs and various other Dictionary Values, encoding may be necessary. The default/assumption is that all Dictionary Values should be encoded when retrieved/rendered from the Values Dictionary. However, the `:raw` suffix provides a format for Values to ensure that if they are already encoded, they are not encoded again when rendered. This is often useful when setting the URL property of Content Parts and Pages.

## Values Dictionary

SystemID = 2

ETS.ReturnUrl = /TS/home/hub1

ProductCode = ABC Product

## Expressions

`{ETS.ReturnUrl}`

`{ETS.ReturnUrl:raw}`

`Spoke?SystemID={SystemID}&ReturnUrl={ETS.ReturnUrl}&ProductCode={ProductCode}`

`Spoke?SystemID={SystemID}&ReturnUrl={ETS.ReturnUrl:raw}&ProductCode={ProductCode:raw}`

## Results

%2FTS%2Fhome%2Fhub1

/TS/home/hub1

Spoke?SystemID=2\&ReturnUrl=%2FTS%2Fhome%2Fhub1\&ProductCode=ABC%20Product

Spoke?SystemID=2\&ReturnUrl=/TS/home/hub1\&ProductCode=ABC Product
