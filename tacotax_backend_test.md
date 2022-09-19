# Climb - Backend technical test
## Summary
1. Objective
2. Technologies
3. Specificities
4. Next steps

## Objective :
The main goal is to create a service that would allow us to upload a questionnaire structure in YAML and retrieve this data in JSON format.
In real life these data would be used to build the following questionnaire [service](https://www.weareclimb.fr/analyse-defiscalisation)

Tasks :

1. Make a page to upload a YAML file
2. Make an API endpoint to retrieve the uploaded content in JSON format
3. Implement validations over the content
4. Write some RSPEC test to cover at least one endpoint behaviour


## Technologies :
Ruby on Rails.
Database choice is up to preference.
Rspec for tests.


## Specs :
### Upload
* Upload page, `GET localhost:3000/questionnaires/new` with the possibility to chose the file to upload
* POST `localhost:3000/questionnaires` with chose file
* Validate questionnaire format and structure
* If questionnaire is valid redirect to upload page with flash message `L'upload du questionnaire a réussi`
* If questionnaire is invalid redirect to upload page with the list of errors as an error message

### Element types
* questionnaire :  
  root element, its reference will be used to retrive data through the `GET localhost:3000/questionnaires/:reference` endpoint.  
  Validate presence of reference and content
* slide :  
  represents a "page" of a questionnaire
  validates presence of reference, label and content
* text_input :  
  validates presence of reference, label
* number_input :  
  validates presence of reference, label
* boolean :  
  validates presence of reference, label
* single_choice :
  validates presence of reference, label and two answers
  Valide la présence d'une référence, d'un label, et d'au moins une réponse.  
* multiple_choice :  
  validates presence of reference, label and two answers

### Questionnaire validation
* file must be YAML formatted
* Each questionnaire element should have a type
* Only types described above are allowed
* Each element validates what is described above

### Further
We can discuss
* Choice around questionnaire storage
* How would we implement versionning on the questionnaire ?