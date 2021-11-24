# Interactive Bot for user engagement

## Introduction
Features of the bot:
- Assists the customer in making a purchase
- Offers product recommendations
- Helps the customer in making a return, exchange or refund
- Assists the customer with credit card related issues
- Takes feedback from customer.

(This model was one of the top 26 models in Flipkart Grid 3.0 - Software development track)

## 👷‍ Installation

To install , please clone the repo and run:

```sh
cd rasa-demo
make install
```

This will install the bot and all of its requirements.
Note that this bot should be used with python 3.6 or 3.7.


## 🤖 To run :

Use `rasa train` to train a model (this will take a significant amount of memory to train,
if you want to train it faster, try the training command with
`--augmentation 0`).

Then, to run, first set up your action server in one terminal window:
```bash
rasa run actions --actions actions.actions
```

In another window, run the bot:
```bash
docker run -p 8000:8000 rasa/duckling
rasa shell --debug
```

Note that `--debug` mode will produce a lot of output meant to help you understand how the bot is working 
under the hood. To simply talk to the bot, you can remove this flag.

If you would like to run the bot on your website, follow the instructions
[here](https://github.com/botfront/rasa-webchat) to place the chat widget on
your website.

## To test :

After doing a `rasa train`, run the command:

```bash
rasa test nlu -u test/test_data.json --model models
rasa test core --stories test/test_stories.md
```

## 👩‍💻 Overview of the files

`data/core/` - contains stories 

`data/nlu` - contains NLU training data

`actions` - contains custom action code

`domain.yml` - the domain file, including bot response templates

`config.yml` - training configurations for the NLU pipeline and policy ensemble


## Development

To install requirements for development, run:

```sh
make install-dev
```

To run unit tests for custom actions:

```
make test-actions
```

To ensure proper database cleanup during testing, you will need to include a connection URL for your tracker store database in your .env file e.g.
```
TRACKER_DB_URL=postgresql:///tracker
```
This is not necessary for running the actions.
