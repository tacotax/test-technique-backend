# Tacotax - Backend technical test
## Summary
1. Objective
2. Technologies
3. Specificities
4. Next steps

## Objective :
The main goal is to create a service that would allow us to upload a questionnaire and retrieve its data in JSON format.
In real life these data would be used to build the following [service](https://www.tacotax.fr/defiscalisation/slider)

Tasks :

1. Make an API endpoint that can receive a JSON payload and store it
2. Make an API endpoint to retrieve the uploaded JSON
3. Implement validations over the content
4. Alternative way to upload the data through YAML
5. Write some RSPEC test to cover at least one endpoint behaviour


## Technologies :
Ruby on Rails
Database choice is up to preference
Rspec for unit tests


## Tasks details :

### 1. Make an API endpoint that can receive a JSON payload and store it

Implement an endpoint POST `localhost:3000/questionnaires` with body

```
{
  payload:
    CONTENT_OF_THE_JSON_EXAMPLE_FILE
}
```

Store the data somewhere, we should be able to retrieve it using the root reference of the JSON example

### 2. Make an API endpoint to retrieve the uploaded JSON

Implement an endpoint GET `localhost:3000/questionnaires/:reference` to retrieve the content of the JSON store under the given `:reference`

### 3. Implement validations over the content

The content can be divided into the following types :
- questionnaire :
  should validate presence of `reference` and `content`. `content` should contain at least one slide
- slide :
  represents one "page" of questionnaire
  should validate presence of `reference`, `label` and `content`. `content` should contain at least one of the following elements
- text_input :
  should validate presence of `reference` and `label`
- number_input :
  should validate presence of `reference` and `label`
- boolean :
  should validate presence of `reference` and `label`
- single_choice :
  should validate presence of `reference`, `label` and `content`. `content` should validate the presence of at least one response element
- multiple_choice :
  should validate presence of `reference`, `label` and `content`. `content` should validate the presence of at least one response element
- response element :
  should validate presence of `label` and `value`


### 4. Alternative way to upload the data through YAML

Create a page GET `localhost:3000/questionnaires/new` where you can select a file.
You can then update the file and the content get store as JSON.
The upload should only allow for YAML files (see given example).
The YAML should be converted to JSON and stored.
