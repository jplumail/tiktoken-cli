# tiktoken-cli

Simple wrapper around [tiktoken](https://github.com/openai/tiktoken) to use
it in your favorite language.

## Why

If you play with openAI's GPT API, you probably encounter one annoying
problem : your prompt is allowed a given amount of tokens, you have no
idea how those tokens are counted, and you only know it was too much when
the API replies with an error, which is seriously annoying (and slow).

OpenAI published its [tiktoken](https://github.com/openai/tiktoken) token
counting library to solve that, which helps a lot! If you're writing a
python program.

`tiktoken-cli` allows you to write your program in any language. It's a
simple wrapper around `tiktoken` that will read your prompt from STDIN and
write the tokens to STDOUT. Now you can write your program in
your favorite language and use the CLI for token counting.

It's almost not worth publishing a github repos for so few lines, but I
figured that README explanation would be valuable for people wondering how
to use openAI's API in their favorite language, the code is merely an
executable example.

A note for those of you who may be new to GPT's API : having the count of
tokens from your prompt alone is not enough to avoid the exceed context
errors. This is because the API wraps your messages with its own content.
The exact algorithm to know if you're going to exceed the count is
documented [in the API doc here](https://platform.openai.com/docs/guides/chat)
(it's in the block "Deep dive : Counting tokens for chat API calls").

## Install

`tiktoken-cli` is a simple script, you can install via pipx.

```shell
pipx install tiktoken-cli
```

## Usage

To use `tiktoken` send your prompt as STDIN, and read the tokens
as STDOUT.

Examples:

In shell:

```shell
tiktoken --model gpt-4 in.txt out.txt
```

Replace the file with `-` for standard input/output:

```shell
echo "Hello, world!" | tiktoken --model gpt-4 - out.txt # writes tokens to out.txt
tiktoken --model gpt-4 in.txt - # writes tokens to stdout
```

You can count tokens easily:

```shell
echo "Hello, world!" | tiktoken - | wc -l
```

## Model

`tiktoken` counts tokens differently based on model. By default, the model
used is gpt-3.5-turbo.

You can change the model using the `--model` option.

For the full list of models available:
```shell
tiktoken --help
```