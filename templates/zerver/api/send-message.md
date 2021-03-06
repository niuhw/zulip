# Send a message

{generate_api_description(/messages:post)}

## Usage examples

{start_tabs}
{tab|python}

{generate_code_example(python)|/messages:post|example}

{tab|js}

More examples and documentation can be found [here](https://github.com/zulip/zulip-js).

{generate_code_example(javascript)|/messages:post|example}

{tab|curl}

``` curl
# For stream messages
curl -X POST {{ api_url }}/v1/messages \
    -u BOT_EMAIL_ADDRESS:BOT_API_KEY \
    -d "type=stream" \
    -d "to=Denmark" \
    -d "subject=Castle" \
    -d $"content=I come not, friends, to steal away your hearts."

# For private messages
curl -X POST {{ api_url }}/v1/messages \
    -u BOT_EMAIL_ADDRESS:BOT_API_KEY \
    -d "type=private" \
    -d "to=[9]" \
    -d $"content=With mirth and laughter let old wrinkles come."
```

{tab|zulip-send}

You can use `zulip-send`
(available after you `pip install zulip`) to easily send Zulips from
the command-line, providing the message content via STDIN.

```bash
# For stream messages
zulip-send --stream Denmark --subject Castle \
    --user othello-bot@example.com --api-key a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5

# For private messages
zulip-send hamlet@example.com \
    --user othello-bot@example.com --api-key a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5
```

#### Passing in the message on the command-line

If you'd like, you can also provide the message on the command-line with the
`-m` or `--message` flag, as follows:


```bash
zulip-send --stream Denmark --subject Castle \
    --message "I come not, friends, to steal away your hearts." \
    --user othello-bot@example.com --api-key a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5
```

You can omit the `user` and `api-key` arguments if you have a `~/.zuliprc`
file.

{end_tabs}

## Arguments

{generate_api_arguments_table|zulip.yaml|/messages:post}

## Response

#### Return values

* `id`: The ID of the newly created message

#### Example response
A typical successful JSON response may look like:

{generate_code_example|/messages:post|fixture(200)}

A typical failed JSON response for when a stream message is sent to a stream
that does not exist:

{generate_code_example|/messages:post|fixture(400_0)}

A typical failed JSON response for when a private message is sent to a user
that does not exist:

{generate_code_example|/messages:post|fixture(400_1)}
