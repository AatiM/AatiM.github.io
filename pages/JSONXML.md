---
title: JSON/XML
permalink: /jsonxml/
---

# Documenting JSON & XML

In some projects, technical writers are supposed to document JSON or XML. In here, I have tried to write a very simple example in order to show how I can fulfill this task.

Imagine I have written a comment in a blog. This is what is happening behind the scene.

### Documenting JSON

```json
{
  "comment": {
    "userId": "Aati",
    "discussionId": 9847892903748,
    "time": "2020-03-23 10:08:32",
    "text": "Merry Christmas "
  }
}
```

| Element | Description | Type | Required | Notes |
|:--------|:-------|:--------|:---------|:-------|
| comment | Top level  | comment data object   | Required |
|======
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;userId  | The ID of the user making the comment  | string   | Required |
|=====
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;discussionId   | The ID of the discussion that is being commented on   | number | Required |
|=======
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;time | The time the comment was posted | string | Optional | Time is GMT. Format is YYYY-MM-DD HH:MM:SS Default is the time the comment is received by the server. |
|=======
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;text | The text of the comment | string | Required |
|=======
{: rules="groups"}

### Documenting XML

``` xml
<?xml version="1.0" encoding="UTF-8" ?>
<song language="en">
    <title>Black and Blue</title>
    <artist>The Rolling Stones</artist>
    <musicians>
        <musician>Mike Jagger<musician>
        <musician>Mike Taylor<musician>
        <musician>Brian Jones<musician>
        <musician>Ian Stewart<musician>
    </musiscians>
</song>
```

| Element| Description | Type | Notes |
|:--------|:-------|:--------|:-------|
| song   | Top level   | song data object   | Attributes: language: Two letter language code |
|======
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; title   | Song title   | string   |
|=====
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; artist   | Song artist   | string |
|======
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;musicians | A list of musicians who play on the song | JSON: array of string / XML: array of musician elements |
|======
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;musician | The number of the musician |
|======
{: rules="groups"}
