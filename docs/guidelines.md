# **Guidelines for iKAT 2025 Year 3** 

The guidelines for iKAT 2024 (year 2) are now available as a [**Google Doc**](https://docs.google.com/document/d/1S0_HpzTg1WKQ4mx7ps6d3-ChB9dmmtk8YPyYjCsZv_4/edit?usp=sharing).

The guidelines for iKAT 2023 (year 1) are also available as a [**Google Doc**](https://docs.google.com/document/d/1dso0VANm5Q08UWt4ppZvzvH6zkpRhfoukwpBgeJNbHE/edit?usp=sharing).

---

## **Participation**

Participants [must register](https://ir.nist.gov/evalbase/accounts/login/?next=/evalbase/) to submit. To request a late registration, please email [trec@nist.gov](mailto:trec@nist.gov) requesting a registration key. The dissemination form must be returned to submit runs.

As a result of the registration, participants will receive an access token with which participants can authenticate themselves to be able to use the simulation API in order to participate in the interactive task. 

## **Motivation**

The TREC Interactive Knowledge Assistance Track (iKAT) aims to advance research on collaborative information-seeking conversational agents that generate personalized responses by leveraging information learned about the user. 

In iKAT, the conversation progresses not only based on prior system responses but also on personal user information. As a result, given the same topic, users with different profiles may follow distinct conversational paths, influencing acceptable system responses for the same underlying information need. With the advent of large language models (LLMs), this task is especially timely—raising new challenges in integrating personalization through context-aware prompting, dynamic interaction, and mixed-initiative dialogue. 


## **Track Overview**

In iKAT, the next turn of a conversation is influenced by the following aspects. 

1. The previous responses from the system and utterances from the user. 
2. The given persona of the user. 
3. The information revealed by the user during the conversation (background, perspective, previous conversations, and context).  

The persona of the user and their corresponding information needs dictate the direction of a conversation. Each user is assigned a distinct persona and will engage in multiple conversations across different topics. For different users, different system responses are acceptable, which demonstrates the personalized nature of the conversations. To this end, the persona and the information needs of the user are modeled by generating a Personal Textual Knowledge Base (PTKB) which is available to the system during the conversation.  

## **What’s New?** 

* **Interactive Submissions**: In Year 3, iKAT is introducing interactive submissions where participants are given access to an API endpoint and will be interacting with a live simulation system on each topic. More details can be found [here](#new-interactive-submissions). 
* **Multiple dialogues per user persona**: To make the task more realistic and challenging, we are including multiple dialogues per user. This will require long-term memory or dynamic PTKB modeling by the participants to effectively address the user’s needs spread across multiple dialogues. 
* **Dynamic PTKBs**: As also mentioned earlier, this year’s edition will encourage teams to actively extract and store new PTKB statements from the dialogues to be able to use them in the future dialogues. More details can be found [here](#ptkb-statement-provenance-classification). 

## **Task Overview**

In Year 3, the following inputs are provided to the participants at each conversation turn: 

1. Personal Text Knowledge Base (PTKB);
2. Conversation history (user utterance and system response for previous turns);
3. The current user utterance.

### **Submission Classes**

We offer the following tasks:

#### **Offline Submissions**

- **Passage Ranking & Response Generation**: For each turn, retrieve and rank relevant passages from the given collection in response to the last user utterance. Then use the ranked passages to generate and return a set of responses, for example using a Retrieval-Augmented Generation (RAG) pipeline. All responses must have at least one passage called “provenance” from the collection.
- **(Only) Response Generation**: For each turn, given a ranked list of passages, return a set of responses. Hence, in this task, you are provided with the passage provenances and you do not have to do any ranking. You will only submit the generated responses for each conversational turn. 

#### <span style="color: darkred">(New!!)</span> **Interactive Submissions**
- **Passage Ranking & Interactive Response Generation**: For each real-time simulated user turn, retrieve and rank relevant passages from the given collection. Then use the ranked passages to generate a personalized response. This response will be passed back to the simulated user, which again produces an utterance. This process will be repeated until the user terminates the conversation. 

For both submission types (offline and interactive) we also offer the PTKB Classification Task:  

- **PTKB Statement Classification**: For each turn, given the PTKB, return a list of the relevant PTKB statements. This task is essentially a binary classification task. So, the output required is a list of relevant statements from the PTKB. 

We will provide baseline passage ranking and response generation methods for each of the tasks.

**Note**: We do not have manual submission runs this year.


## **Example Dialogue Tree**

An example of two different conversations based on different personas for the same topic is shown in the following figure. For each user turn, systems should return a ranked list of text responses. Each response has one or more (ranked) source passages as provenance. In addition, the systems should provide a sorted list of relevant statements of PTKB with the corresponding relevance score.

![Picture depicting a conversation tree](conversation-tree.jpg)

Below, we provide a detailed explanation of the above diagram. 
<table>
<tr>
	<th>Turn</th>
	<th>Field</th>
	<th>Value</th>
</tr>

<tr>
	<td colspan="3" style="text-align: center"><b>Topic 1-1, PTKB_1</b></td>
</tr>


<tr>
	<td rowspan="4">1</td>
	<td>User utterance</td>
	<td>I want to start my master’s degree, can you help me with finding a university? </td>
</tr>
<tr>
	<td>Response</td>
	<td>Do you want to continue your bachelor’s studies and obtain a degree in computer science? </td>
</tr>
<tr>
	<td>Citations</td>
	<td>Null</td>
</tr>
<tr>
	<td>Relevant PTKBs</td>
	<td>
		<ul>
			<li>I have a bachelor’s degree in computer science from Tilburg University</li>
		</ul>
	</td>
</tr>


<tr>
	<td rowspan="4">2</td>
	<td>User utterance</td>
	<td>Yes, I want to continue my studies in computer science.</td>
</tr>
<tr>
	<td>Response</td>
	<td>Do you want to study abroad?</td>
</tr>
<tr>
	<td>Citations</td>
	<td>Null</td>
</tr>
<tr>
	<td>Relevant PTKBs</td>
	<td>
		<ul>
			<li>I live in the Netherlands</li>
		</ul>
	</td>
</tr>


<tr>
	<td rowspan="4">3</td>
	<td>User utterance</td>
	<td>No, I don't want to go abroad.</td>
</tr>
<tr>
	<td>Response</td>
	<td>
		I can help you find a university to continue your studies in the Netherlands as a computer science student. Take a look at these Top Computer Science Universities in the Netherlands:
		<ul>
			<li>Delft University of Technology.</li>
			<li>Eindhoven University of Technology.</li>
			<li>Vrije Universiteit Amsterdam.</li>
			<li>University of Amsterdam.</li>
			<li>Leiden University.</li>
			<li>Radboud University.</li>
			<li>Utrecht University.</li>
			<li>University of Twente.</li>
		</ul>
	</td>
</tr>
<tr>
	<td>Citations</td>
	<td><tt>clueweb22-en0034-09-03452:0</tt></td>
</tr>
<tr>
	<td>Relevant PTKBs</td>
	<td>
		<ul>
			<li>I live in the Netherlands</li>
			<li>I have a bachelor’s degree in computer science from Tilburg University</li>
		</ul>
	</td>
</tr>


<tr>
	<td rowspan="4">4</td>
	<td>User utterance</td>
	<td>Which are the best three?</td>
</tr>
<tr>
	<td>Response</td>
	<td>
		Based on the ranking of research.com the top three universities are as follows: 
		<ol>
			<li>Delft University of Technology.</li>
			<li>University of Amsterdam.</li>
			<li>Eindhoven University of Technology.</li>
		</ol>
	</td>
</tr>
<tr>
	<td>Citations</td>
	<td><tt>clueweb22-en0016-21-09213:0 </tt></td>
</tr>
<tr>
	<td>Relevant PTKBs</td>
	<td>
		<ul>
			<li>I live in the Netherlands</li>
			<li>I have a bachelor’s degree in computer science from Tilburg University</li>
		</ul>
	</td>
</tr>

<tr>
	<td colspan="3" style="text-align: center"><b>Topic 1-2, PTKB_2</b></td>
</tr>


<tr>
	<td rowspan="4">1</td>
	<td>User utterance</td>
	<td>I want to start my master’s degree, can you help me with finding a university? </td>
</tr>
<tr>
	<td>Response</td>
	<td>
		Sure, do you want to study computer science?
	</td>
</tr>
<tr>
	<td>Citations</td>
	<td>Null</td>
</tr>
<tr>
	<td>Relevant PTKBs</td>
	<td>
		<ul>
			<li>I have a bachelor’s degree in computer science with a GPA of 3.3 out of 4.0 </li>
		</ul>
	</td>
</tr>


<tr>
	<td rowspan="4">2</td>
	<td>User utterance</td>
	<td>Yes, I want to pursue my education in computer science. Can you tell me the names of the best universities?</td>
</tr>
<tr>
	<td>Response</td>
	<td>
		Here are the best universities for computer science in Canada: 
		<ol>
			<li>University of British Columbia</li>
			<li>University of Alberta</li>
			<li>Concordia University</li>
			<li>Simon Fraser University</li>
			<li>The University of Toronto</li>
		</ol>
	</td>
</tr>
<tr>
	<td>Citations</td>
	<td><tt>clueweb22-en0026-31-15538:1</tt><br> <tt>clueweb22-en0026-31-15538:4</tt><br><tt>clueweb22-en0026-31-15538:6</tt><br><tt>clueweb22-en0040-41-06056:0</tt></td>
</tr>
<tr>
	<td>Relevant PTKBs</td>
	<td>
		<ul>
			<li>I have a bachelor’s degree in computer science with a GPA of 3.3 out of 4.0</li>
			<li>I’m moving to Canada to study master</li>
		</ul>
	</td>
</tr>


<tr>
	<td rowspan="4">3</td>
	<td>User utterance</td>
	<td>Which of them best suits me in terms of weather conditions?</td>
</tr>
<tr>
	<td>Response</td>
	<td>
		University of British Columbia in Vancouver has temperatures near 80 degrees Fahrenheit (27 degrees Celsius) in summer and up to 45 degrees Fahrenheit (about 7 degrees Celsius) in winter which is suitable for you.<br>
		The University of Toronto is acceptable since it has cold winters, average temperatures can drop below -10 ° C but not below 12 degrees for long.<br>
		The Concordia University in Montreal is not suitable for you since in the winter, it could reach minus 40 with the wind chill. <br>
		The University of Alberta is also not suitable for you. In winter the average temperature varies between -6.5°C (20.3°F) and -13.5°C (7.7°F). <br>
		Simon Fraser University is not acceptable to you. The city in which the university is located will reach temperatures of -14 in the winter.
	</td>
</tr>
<tr>
	<td>Citations</td>
	<td><tt>clueweb22-en0000-94-02275:0</tt><br>
   		<tt>clueweb22-en0027-06-08704:1</tt><br>
		<tt>clueweb22-en0005-63-12144:0</tt><br>
		<tt>clueweb22-en0013-01-17558:1</tt><br>
		<tt>clueweb22-en0014-39-04143:0</tt>
   </td>
</tr>
<tr>
	<td>Relevant PTKBs</td>
	<td>
		<ul>
			<li>I cannot withstand the temperatures below -12 for a long time </li>
			<li>I’m used to heavy rains in the Netherlands</li>
		</ul>
	</td>
</tr>


<tr>
	<td rowspan="4">4</td>
	<td>User utterance</td>
	<td>Can you tell me more about the University of Toronto?</td>
</tr>
<tr>
	<td>Response</td>
	<td>
		Sure, what do you want to know about? Do you want to know about its campus, community, or programs? 
	</td>
</tr>
<tr>
	<td>Citations</td>
	<td>Null</td>
</tr>
<tr>
	<td>Relevant PTKBs</td>
	<td>
		Null
	</td>
</tr>
</table>


## **Primary Task Details**

The main aim of iKAT can be defined as **personalized retrieval-based “candidate response generation” in the context of a conversation and a set PTKB statements**. A detailed explanation of the subtasks is provided in the following. 

### **PTKB Statement (provenance) Classification**
- This task is a binary classification problem. The output is a list of the statements from PTKB that are relevant for responding to the user’s utterance. 
- The provenance PTKB statements can be an empty list for some responses.
- The PTKB statements can be taken from the given list of PTKB statements, or extracted from previous user conversations. 
- <span style="color: darkred">(New!!)</span> New PTKB statements can be extracted from the previous conversations and mentioned in the list of relevant PTKB statements. 

### **Passage Ranking (citation)**
- The provided context for passage ranking per each user utterance includes:
  	- A fixed set of previous utterances and responses in the preceding turns up to the current step, 
    - PTKB of the user provided at the beginning of the conversation, 
    - The previous conversation of the same user with the system.  
      **Note**: this information is only important for a better (or updated) understanding of the persona of the user and the information need of the user in the current turn is not dependent on the previous conversations.
- **Note**: Using information from 1) following turns and 2) the relevant PTKB statements from previous turns **is not allowed**.  
- A run must include the provenance passages retrieved by the retrieval model (called “references” in the submission format) for all turns of the conversation. 
- The “reference” field is a list of the top 1000 passages retrieved by the retrieval model based on their relevance. The passages must be included in this field using the format `doc_id:passage_id`.
- The first 1000 provenance passages for each turn will be assessed.
- **Note**: for each turn of the conversation, there is only one “reference” field in the submission format. This means that the participants are only allowed to submit one ranked list of the passages for each turn. 


### **Response Generation**
- Each response can be generated from multiple passages. It can be an abstractive or extractive summary of the corresponding passages, or a text generated by a Retrieval-Augment Generation (RAG) model. 
- Each response must have one or more passages as provenance from the collection used to produce it. 
- A run can have multiple responses for each turn. We will assess just the first response (or the response with “rank=1”) for each turn. 
- The passages used for generating each response must be mentioned in the “citations” field using the format `doc_id:passage_id`.  
- We will not evaluate the responses without any provenance passages (i.e. an empty list of “citations”). 
- Because a response may have multiple source passages, the score of passages in the citations list for a response is used to order passages in descending order. 
- A response is a text suitable for showing to the user. It should be fluent, satisfy their information needs, and not contain extraneous or redundant information.  
- A response is limited to a **maximum of 250 words** (as measured by the `Tokenizer` function of `spacy.tokenizer` in spaCy v3.3 library) but should vary depending on an appropriate query-response. 

### <span style="color: darkred">(New!!)</span> **Interactive Response Generation**

- Conversations in this task are always user initiated. After submitting run meta information to the simulation API, participants receive the first user utterance.
- Participant systems should retrieve relevant passages from the collection based on the utterance and generate a response. The ranked list of passages and the generated response should be sent back to the simulation API.
- Sending back the passages and the response results in a new user utterance provided by the API on the same topic to which the participant system should respond again.
- This process is repeated until the user indicates (through a flag, `last_response_of_session`) that they terminate the current session.
- The next request of a participant system then leads to a user utterance for a new session on a new topic with a (potential) new user.
- This process is repeated until all topics in the test set have been addressed, which will also be indicated through a flag in the API. 
- After all topics have been addressed, the run counts as submitted (no additional submission of a run file required).   
- Responses from the simulation API contain identifiers to differentiate with which user the participants system currently talks with. This allows participants to track PTKB statements of reoccurring users. If participants track PTKB statements they can provide relevant statements through the API as well.
- Responses for this task should satisfy the same properties as for the (non-interactive) response generation task. 
- This task invites participants to apply various techniques to clarify information needs like asking clarifying questions or preference elicitation. <br> **Note**: Attempts at jailbreaking to reveal system details or to try to make the user simulator behave in an unintended way will result in disqualification.

Technical documentation on how to operate the API will be released soon. However, a sample interaction with the simulation API can be found below.

#### API Output Example
```json
{ 
  "timestamp":"2025-05-06T10:58:33.400920", 
  "run_id":"my_best_run_02", 
  "topic_id":"1-1", 
  "user_id":"f3333f5c-8313-4941-beea-f24de25a583a", 
  "utterance":"Show me universities with computer science programs.", 
  "history":[ 
    { 
      "role":"user", 
      "content":"Show me universities with computer science programs." 
    } 
  ], 
  "last_response_of_session":false, 
  "last_response_of_run":false 
} 
```

#### API Input Example
```json
{ 
  "run_id":"my_best_run_02", 
  "response":"There is University of Amsterdam.", 
  "citations":{ 
    "clueweb22-en0032-04-00208:7":0.8, 
    "clueweb22-en0027-84-11778:0":0.4 
  }, 
  "relevant_ptkbs":[ 
    "I live in the Netherlands." 
  ] 
} 
```

## **Collection**

The text collection contains a subset of ClueWeb22 documents, prepared by the organizers in collaboration with CMU. Documents have then been split into ~116M passages. The goal is to retrieve passages from target open-domain text collections. 

### **License for ClueWeb22-B**

Getting the license to use the collection can be time-consuming and would be handled by CMU, not the iKAT organizers. Please follow these steps to get your data license ASAP: 

- Sign the license form available on the ClueWeb22 project [web page](https://lemurproject.org/clueweb22/obtain.php) and send the form to CMU for approval ([clueweb@andrew.cmu.edu](mailto:clueweb@andrew.cmu.edu)).

- Once you have the license, send a mail to Andrew Ramsay ([andrew.ramsay@glasgow.ac.uk](mailto:andrew.ramsay@glasgow.ac.uk)) to have access to a download link with the preprocessed iKAT passage collection, and other resources such as Lucene and SPLADE indices. 

Please give enough time to the CMU licensing office to accept your request.

- CMU requires a signature from the organization (i.e., the university or company), not an individual who wants to use the data. This can slow down the process at your end too. So, it’s useful to start the process ASAP.
- If you already have an accepted license for ClueWeb22, you do not need a new form. Please let us know if that is the case.
- As an alternative for (2), once you have access to ClueWeb22, you can get the raw ClueWeb22-B/iKAT collection yourself with the license, and do all passage-segmentation yourself, but we advise you to use our processed version to avoid any error.

Please do feel free to reach out to us if you have any questions or doubts about the process, so we can prevent any delays in getting the data to you.


### **Passage Segmentation**

For assessment, we will judge provenance passages. We segment the documents in our collection into passages in a similar manner as done by the TREC Deep Learning track for segmenting MS MARCO documents into passages: First, each document is trimmed to 10k characters. Then a 10-sentence sliding window with a 5-sentence stride is used to generate the passages.  

An example document with some passage segmentation is provided in TrecWeb format below for illustration purposes: 

```xml
<DOC>
	<DOCNO>clueweb22-en0020-70-00000</DOCNO>
	<DOCHDR></DOCHDR>
	<HTML>
		<TITLE>06AECE252028B717019F2802EB065B68</TITLE>
		<URL>https://pokemon.fandom.com/wiki/Donphan</URL>
		<BODY>
			<PASSAGE id=0>
				It has thin, elongated ears held out almost perpendicular to its
				body. Its four short legs...
			</PASSAGE>
			<PASSAGE id=1>
				It has been demonstrated that Donphan has a keen sense of smell,
				capable of sniffing out a gem known as amberite. Donphan...
			</PASSAGE>
		</BODY>
	</HTML>
</DOC>
```

### **Provided ClueWeb22 Indices**

As of now, our resource includes a BM25 Pyserini index of the collection, and a SPLADE index of the collection. 

The SPLADE index was made with the numba library, as in the original [SPLADE github](https://github.com/naver/splade), and can be re-used for retrieval. It uses the [SPLADE++ model](https://huggingface.co/naver/splade-cocondenser-ensembledistil). 

[//]: # (![Picture depicting passage segmentation for iKAT]&#40;passage-segmentation.png&#41;)

## **Topics**

We will provide several sample topics with example baseline runs for validation and testing. Below is a sample topics file from two different personas on the same topic. The `conv_id` represents a concatenation of the persona and topic id `<persona_id>-<topic_id>`. Also, a `citation` field with a list of provenance passages and a `ptkb_provenance` field with a list of provenance statements from PTKB are included. These two fields define the trajectory of the conversation and should be used for generating responses in the offline response generation task.  

```json
[
  {
    "conv_id": "1-1",
    "title": "Finding a University",
    "ptkb": [
      "I graduated from Tilburg University.",
      "I live in the Netherlands.",
      "I'm allergic to peanuts.",
      "I worked as a web developer for 2 years.",  
      "I have a bachelor's degree in computer science.",  
      "I like Indian food.",  
      "My bachelor's GPA is 5.6.",  
      "I'm 26 years old.",  
      "My TOEFL SCORE is 91.",  
      "My interesting bachelor courses are data structure, algorithm, data mining, and artificial intelligence.",  
      "I didn't like computer architecture and logical circuits courses."  
    ],  
    "responses": [  
      {  
        "turn_id": 1,  
        "user_utterance": "I want to start my master's degree, can you help me with finding a university?",  
        "resolved_utterance": "I want to start my master's degree, can you help me with finding a university?",  
        "response": "Do you want to continue your bachelor's studies and obtain a degree in computer science?",  
        "ptkb_provenance": [  
          "I have a bachelor's degree in computer science." 
        ],
        "citations": [  
          "clueweb22-en0034-09-03452:1",  
          "clueweb22-en0034-09-03452:3",  
          "clueweb22-en0034-09-03452:5",  
          "clueweb22-en0034-09-03452:7",  
          "clueweb22-en0034-09-03452:9"  
        ]  
      },  
      {  
        "turn_id": 2,  
        "user_utterance": "Yes, I want to continue my studies in computer science.",  
        "resolved_utterance": "Yes, I want to continue my studies in computer science.",  
        "response": "Do you want to study in the Netherlands, Europe, or somewhere further away?",  
        "ptkb_provenance": [  
          "I live in the Netherlands." 
        ],
        "citations": [  
          "clueweb22-en0034-09-03452:2",  
          "clueweb22-en0034-09-03452:4",  
          "clueweb22-en0034-09-03452:6",  
          "clueweb22-en0034-09-03452:8",  
          "clueweb22-en0034-09-03452:10"  
        ]  
      },  
      {  
        "turn_id": 3,  
        "user_utterance": "I'd like to stay here.",  
        "resolved_utterance": "I'd like to stay in the Netherlands.",  
        "response": "I can help you with finding a university for continuing your studies in the Netherlands as a computer science student. Take a look at these Top Computer Science Universities in the Netherlands: Delft University of Technology, Eindhoven University of Technology, Vrije Universiteit Amsterdam, University of Amsterdam, Leiden University, Radboud University, Utrecht University, University of Twente",  
        "ptkb_provenance": [  
            "I have a bachelor's degree in computer science.", 
            "I live in the Netherlands." 
        ],
        "citattions": [  
          "clueweb22-en0012-00-00012:0",  
          "clueweb22-en0012-00-00012:1",  
          "clueweb22-en0012-00-00012:2",  
          "clueweb22-en0012-00-00012:3",  
          "clueweb22-en0012-00-00012:4"  
        ]  
      }  
    ]  
  },  
  {  
    "conv_id": "2-2",  
    "title": "Finding a university",  
    "ptkb": [  
     "I don't like crazy cold weather.",  
      "I don't have a driver's license.",  
      "I plan to move to Canada.",  
      "I'm from the Netherlands.",  
      "I'm used to heavy rains in the Netherlands.",  
      "I graduated from UvA.",  
      "I have bachelor's degree in computer science.",  
      "I speak English fluently."  
    ],  
    "responses": [  
      {  
        "turn_id": 1,  
        "user_utterance": "I want to start my master's degree, can you help me with finding a university?",  
        "resolved_utterance": "I want to start my master's degree, can you help me with finding a university in Canada?",  
        "response": "Sure, do you want to study computer science?",  
        "ptkb_provenance": [  
          "I have bachelor's degree in computer science.",   
          "I plan to move to Canada." 
        ],
        "citations": [  
          "clueweb22-en0040-41-06056:0",  
          "clueweb22-en0040-41-06056:1",  
          "clueweb22-en0040-41-06056:2",  
          "clueweb22-en0040-41-06056:3",  
          "clueweb22-en0040-41-06056:4"  
        ]  
      },  
      {  
        "turn_id": 2,  
        "user_utterance": "Yes, I want to pursue the same major. Can you tell me the name of the best universities?",  
        "resolved_utterance": "Yes, I want to pursue computer science. Can you tell me the name of the best computer science universities in Canada?",  
        "response": "Here are the top universities for computer science in Canada: 1) University of British Columbia, 2) University of Alberta, 3) Concordia University, 4) Simon Fraser University, 5) The University of Toronto",  
        "ptkb_provenance": [],  
        "citations": [  
          "clueweb22-en0026-31-15538:1",  
          "clueweb22-en0026-31-15538:4",  
          "clueweb22-en0026-31-15538:6",  
          "clueweb22-en0040-41-06056:0"  
        ]
      },  
      {  
        "turn_id": 3,  
        "user_utterance": "Which of them best suits me in terms of weather conditions?",  
        "resolved_utterance": "Which of the following universities best suits me in terms of weather conditions? 1) the University of British Columbia, 2) the University of Alberta, 3) Concordia University, 4) Simon Fraser University, and 5) The University of Toronto.",  
        "response": "I know you don't like very cold weather, but can you give me an estimation of the temperature that is acceptable for you?",  
        "ptkb_provenance": [  
          "I don't like crazy cold weather.",  
          "I'm used to heavy rains in the Netherlands." 
        ],
        "citations": [  
          "clueweb22-en0030-30-30030:0",  
          "clueweb22-en0030-30-30030:1",  
          "clueweb22-en0030-30-30030:2",  
          "clueweb22-en0030-30-30030:3",  
          "clueweb22-en0030-30-30030:4"  
        ]  
      }  
    ]  
  }  
]
```

### **Sample Topics**

We are releasing two sample conversations on the topic "Finding a University". Each conversation pertains to a different persona, and the conversation is personalized to that persona. You can find the sample topic [here](https://drive.google.com/file/d/1ZdVXNqnzP1XpYpJejIRn3pzva8Pke9v_/view).  

Those eager to start developing and experimenting can also use the data from previous years of TREC CAsT and TREC iKAT 2023 and 2024 that is available [here](https://www.trecikat.com/additional_data/). 


## **Task Submissions**

Participants submit the output of their system on the specified “test” topics.  A single participant can submit a maximum of: 

- 4 automatic runs, 
- 2 generation-only runs,
- 2 interactive runs.

In the automatic runs, the participants can include response generation based on their own ranking, but this is not mandatory.

In the generation-only run, the participants **must use** the given passage provenances. 

We have three submission classes for each of the 1) automatic, 2) generation-only, and 3) interactive tasks. An example of the submission template for each class of submission is below.  

### **Sample submission for the offline task**

```json
{ 
  "metadata":{ 
    "team_id":"my_favourite_team", 
    "run_id":"my_best_run_02", 
    "run_type":"automatic", 
    "topic_id":"1-2_3" 
  }, 
  "responses":[ 
    { 
      "rank":1, 
      "text":"The University of British Columbia in Vancouver has temperatures near 80 degrees Fahrenheit (27 degrees Celsius) in summer and up to 45 degrees Fahrenheit (about 7 degrees Celsius) in winter which is suitable for you. The university of Toronto is acceptable since has cold winters, average temperatures can drop below -10 ° C but not below 12 degrees for long. The Concordia university in Montreal is not suitable for you since in the winter, could reach minus 40 with the wind chill. University of Alberta is also not suitable for you. In winter the average temperature varies between -6.5°C (20.3°F) and -13.5°C (7.7°F). Simon Fraser university is not acceptable for you. The city which the university is located in will reach temperatures of -14 in the winter.", 
      "citations":{ 
        "clueweb22-en0000-94-02275:0":0.6, 
        "clueweb22-en0027-06-08704:1":0.5, 
        "clueweb22-en0005-63-12144:0":0.4 
                  }, 
      "ptkb_provenance":[ 
        "I cannot withstand the temperatures below -12 for a long time", 
        "I’m used to heavy rains in the Netherlands" 
      ] 
    }, 
    { 
      "rank":2, 
      "text":" The University of British Columbia and Simon Fraser University are the best fits, as Vancouver's mild, rainy winters are similar to the Netherlands. The University of Toronto is colder and snowier but still manageable. Concordia University and the University of Alberta have much harsher winters and would likely feel too cold for your preferences. ", 
      "citations":{ 
        "clueweb22-en0001-23-18493:4":0.8, 
        "clueweb22-en0028-93-98372:9":0.3 
	  }, 
      "ptkb_provenance":[ 
        "I cannot withstand the temperatures below -12 for a long time", 
        "I’m used to heavy rains in the Netherlands" 
	  ]
     }
  ], 
  "references": {
	  "clueweb22-en0000-94-02275:0": 0.6,
	  "clueweb22-en0027-06-08704:1": 0.5,
	  "clueweb22-en0005-63-12144:0": 0.4,
	  "clueweb22-en0001-23-18493:4": 0.8,
	  "clueweb22-en0028-93-98372:9": 0.3
  } 
 }
```

- The `run_id` is a run submission identifier that should be descriptive and unique to your team and institution. 
- The `run_type` is one of the three types “automatic”, “generation-only”, or “interactive”. 
- The `topic_id` is the identifier of each turn of the conversation and has the following format: `{conv_id}_{turn_id}`. For example, `topic_id` of `1-2_3` refers to the turn with `turn_id` of `3` from the conversation with `conv_id` of `1-2`.
- Each turn should also contain a list of `responses`. A response consists of `text` and a `citations` list. The `citations` list is a list of passage provenances used for generating the response. 
- Each turn includes a set of statements from the PTKB in the field called `ptkb_provenance`. It can also contain some statements from previous interactions of the user with the system. 
- The field `references` includes the list of retrieved passages by retrieval model. 
- For the “generation-only” runs, the `reference` field should be empty.

For provenance ranking, this will be converted to a traditional TREC run format: 

```
31_1-1 Q0 clueweb22-en0000-94-02275:0 1 0.5 sample_run
```

Runs may include up to 1000 responses for each user turn. For provenance ranking, only the first 1000 pieces of unique provenance will be used. As in previous year of iKAT, only limited top-k responses and provenances will be assessed according to resource constraints.


## **Evaluation**

We will use the relevance assessment methods used in the previous year of iKAT 2023 for relevance to individual turns. 

1. **Citations Assessment:**     The cited passaged that are used to produce the responses will be pooled and assessed. The relevance scale will be the same as in previous years of CAsT and the first year of iKAT, see the previous overview papers for details. The standard ranking metrics such as P@k, NDCG@k, and MAP will be calculated using the judgments. We will focus on the earlier positions (1, 3, 5). 
2. **Response Assessment:**     A response may be a simple passage or a summary of one or more passages. We will assess the top-ranked response from all systems for a subset of turns. Only responses with at least one citation will be judged. We will assess the quality of generated responses in three different ways. First, we will assess the relevance, naturalness, completeness, and groundedness. Second,  we assess the precision and recall of nuggets of information for the responses. We consider the nugget recall and nugget precision as the coverage and correctness of the responses, respectively. Third, we use surface-based metrics like BLEU and ROUGE to n-gram similarity between the generated response and the manual response. The responses and judgments on them will be released with the judgments. 
3. **Extracted Relevant PTKB Statements Assessment:** The standard metrics like Precision, Recall, and F1 will be used for evaluating the identified list of relevant statements from PTKB. We will assess both pre-defined and newly extracted PTKB statements by the teams. 
4. **Dialogue-level Assessment**: Assessing the whole dialogue and the trajectory in the interactive subtask. Given the flexible nature of the simulated dialogues, we will devise dialogue-level metrics that take into account the system’s capabilities to provide useful information to the users in the dialogue as a whole. These could be based on ideas such as “last-bot-standing”, or returning the most nuggets in the same time budget. More details will follow later. 

Similar to the first two years of iKAT, only a subset of turns may be evaluated for provenance ranking effectiveness and response generation quality. This will be disclosed to participants only after the assessment is completed.

## Related Resources

Below are some useful code resources related to TREC iKAT. 

- Official TREC iKAT Organizer GitHub: 
  	- [https://github.com/irlabamsterdam/iKAT](https://github.com/irlabamsterdam/iKAT)
- Related code and baselines:
  	- [https://github.com/fengranMark/PersonalizedCIR](https://github.com/fengranMark/PersonalizedCIR)
  	- [https://github.com/EricLangezaal/PersonalizedCIR](https://github.com/EricLangezaal/PersonalizedCIR)
  	- [https://github.com/SimonLupart/ikat-2024-baseline](https://github.com/SimonLupart/ikat-2024-baseline)
  	- [https://github.com/shubham526/ikat-2024](https://github.com/shubham526/ikat-2024)



## **Timeline**

Dates are given in the Anywhere on Earth (AoE) timezone.  

| Task               	              |         Date     	 |
|:-----------------------------------|-------------------:|
| Guidelines released                |  May 16, 2025    	 |
| Test topics released               | June 23, 2025    	 |
| Submission deadline                |  July 23, 2025   	 |
| Results released to participants   |    October, 2025 	 |




