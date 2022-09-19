# The-Base

## Project Description

Turning infomration in to knowledge

A programme which allows user to import a text, .jpeg/ .pdf / .docx to extract keywords, a topic and a summary of their text! 

As well, the programme creates a network of keywords in a web so users can navigate and understand how certain texts and their notes relate to one another. 

In the already short time frame we have used API (openAI) to extract keywords and summaries, Wikidata to create hierachies and google cloud language model to extract topics.

We used combination of google and wikipedia to return summaries of keywords. 

## Navigation of Project

../PackageFunction/Package Functions --> contains .py for each tool 

![image](https://user-images.githubusercontent.com/108887806/191011916-d1bd3f1b-e071-464a-8305-7a841292ec91.png)

../api/  --> contains the file for app functions. 

![image](https://user-images.githubusercontent.com/108887806/191012538-71ef594f-0ec9-4dcd-a33c-55cbd30b7fc8.png)


### Keywords

open AI API returning list of first 5 words

def preprocessing_keywords(text):
...
return keywords_final[:5]

### Linking Hierachy 

Linking requires the list of keywords to then create such a hierachy.

The output of the main function is a list, 


def formatting_hierachy(keyword):
    output = get_hierachy(keyword)
    hierachy = []
    counter = len(output)
    counter_up = 0
    for word in list(reversed(output)):
        try:
            if word == hierachy[counter_up]:
                hierachy.pop(counter_up)
        except:
            None
        hierachy.append(word)

        counter = counter - 1
    return hierachy

### Topic extraction

file extracts the topic via using googles langaguge V1 module. 

input the text
and the final function as below.

def topic_slice(classifier_result):
    """Output: Lowest topic in lowercase"""
    list_topics = list(classifier_result.keys())
    topic_list = []

    for i in list_topics:
        topic_list.append(i.split("/"))

    final_list = []
    for n in topic_list:
        final_list.append(n[-1].lower())

    return final_list


## Continued work

Software still in development to improve and refine. Also looking to preseant the results of longer text files in a cleaner . 
