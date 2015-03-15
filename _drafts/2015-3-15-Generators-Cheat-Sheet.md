

| Command | Options | Model | Migration | Controller | Views | Test Suite | Assets (Javascripts, Stylesheets) | Route in config | Helper |
|:----------:|:----------------------------------------------:|:-----:|:---------:|:----------:|:-------------------:|:-----------------:|:---------------------------------:|:---------------:|:------:|
| migration | model name, attributes as name:type | N | Y | N | N | N | N | N | N |
| model | model name, attributes as name:type | Y | Y | N | N | model | N | N | N |
| controller | model name (plural), views | N | N | Y | Y | controller | Y | Y | Y |
| resource | model name, attributes as name:type | Y | Y | Y | folder but no files | controller, model | Y | N | Y |
| scaffold | model name (singular), attributes as name:type | Y | Y | Y | Y | controller, model | Y | Y | Y |

