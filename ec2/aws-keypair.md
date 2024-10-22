# AWS EC2 KEY PAIR Examples

## describe-key-pairs
- describing all the available key pairs  
    - `aws ec2 describe-key-pairs`  
    Output:
        ```
            {
                "KeyPairs": [
                    {
                        "KeyPairId": "key-03188c9c447df3348",
                        "KeyType": "ed25519",
                        "Tags": [],
                        "CreateTime": "2024-10-14T00:06:03.958000+00:00",
                        "KeyName": "jenkins_ec2",
                        "KeyFingerprint": "jJZFc72SPallV2DRc872K31SvK0hFxiskXVCGA2c/5w="
                    },
                    {
                        "KeyPairId": "key-0bac06a768f60a783",
                        "KeyType": "ed25519",
                        "Tags": [
                            {
                                "Key": "Name",
                                "Value": "ec2 key pair"
                            }
                        ],
                        "CreateTime": "2024-10-22T03:27:49.685000+00:00",
                        "KeyName": "ec2_key",
                        "KeyFingerprint": "zpne2qe0PsuUoswSE8lRO2I6hYe+FxVC35ndxnhi/yU="
                    }
                ]
            }
        ```
- Describing only specific key pairs
    - `aws ec2 describe-key-pairs --key_names ec2_key`  
    Output:
        ```
        {
            "KeyPairs": [
                {
                    "KeyPairId": "key-0bac06a768f60a783",
                    "KeyType": "ed25519",
                    "Tags": [
                        {
                            "Key": "Name",
                            "Value": "ec2 key pair"
                        }
                    ],
                    "CreateTime": "2024-10-22T03:27:49.685000+00:00",
                    "KeyName": "ec2_key",
                    "KeyFingerprint": "zpne2qe0PsuUoswSE8lRO2I6hYe+FxVC35ndxnhi/yU="
                }
            ]
        }
        ```
- Describing the key pairs by keypair ids
    - `aws ec2 describe-key-pairs --key-pair-ids key-0bac06a768f60a783`  
    Output
        ```
        {
            "KeyPairs": [
                {
                    "KeyPairId": "key-0bac06a768f60a783",
                    "KeyType": "ed25519",
                    "Tags": [
                        {
                            "Key": "Name",
                            "Value": "ec2 key pair"
                        }
                    ],
                    "CreateTime": "2024-10-22T03:27:49.685000+00:00",
                    "KeyName": "ec2_key",
                    "KeyFingerprint": "zpne2qe0PsuUoswSE8lRO2I6hYe+FxVC35ndxnhi/yU="
                }
            ]
        }
        ```
- Describing the keypairs with public key included
    - `aws ec2 describe-key-pairs --key-names ec2_key --include-public-key`  
        Output
        ```
        {
            "KeyPairs": [
                {
                    "KeyPairId": "key-0bac06a768f60a783",
                    "KeyType": "ed25519",
                    "Tags": [
                        {
                            "Key": "Name",
                            "Value": "ec2 key pair"
                        }
                    ],
                    "PublicKey": "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMxFVC7mE+sNTd+cCtsjh37NBIPzxhdDMuWAIls+CNg2 ec2_key\n",
                    "CreateTime": "2024-10-22T03:27:49.685000+00:00",
                    "KeyName": "ec2_key",
                    "KeyFingerprint": "zpne2qe0PsuUoswSE8lRO2I6hYe+FxVC35ndxnhi/yU="
                }
            ]
        }
        ```

- Describing keypairs using dry run options which checks the user have necessary permissions to make the request
    - `aws ec2 describe-key-pairs --dry-run`

- Describing keypairs with filters
    - `aws ec2 describe-key-pairs --filters Name=key-name,Values=ec2_key Name=key-pair-id,Values=key-0bac06a768f60a783`  
    Output
        ```
            {
                "KeyPairs": [
                    {
                        "KeyPairId": "key-0bac06a768f60a783",
                        "KeyType": "ed25519",
                        "Tags": [
                            {
                                "Key": "Name",
                                "Value": "ec2 key pair"
                            }
                        ],
                        "CreateTime": "2024-10-22T03:27:49.685000+00:00",
                        "KeyName": "ec2_key",
                        "KeyFingerprint": "zpne2qe0PsuUoswSE8lRO2I6hYe+FxVC35ndxnhi/yU="
                    }
                ]
            }
        ```
- Generate cli skeleton with describe-key-pairs the input of the command
    - `aws ec2 describe-key-pairs --generate-cli-skeleton input`   
        Output
        ```
        {
            "KeyNames": [
                ""
            ],
            "KeyPairIds": [
                ""
            ],
            "IncludePublicKey": true,
            "DryRun": true,
            "Filters": [
                {
                    "Name": "",
                    "Values": [
                        ""
                    ]
                }
            ]
        } 
        ```
    - `aws ec2 describe-key-pairs --generate-cli-skeleton output`   
        Output
        ```
        {
            "KeyPairs": [
                {
                    "KeyPairId": "KeyPairId",
                    "KeyType": "KeyType",
                    "Tags": [
                        {
                            "Key": "Key",
                            "Value": "Value"
                        }
                    ],
                    "PublicKey": "PublicKey",
                    "CreateTime": "1970-01-01T00:00:00",
                    "KeyName": "KeyName",
                    "KeyFingerprint": "KeyFingerprint"
                }
            ]
        }
        ```

- Providing the Input to the describe command in JSON format
    - `aws ec2 describe-key-pairs --cli-input-json '{"KeyNames":["ec2_key"]}'`   
        Output:
        ```
        {
            "KeyPairs": [
                {
                    "KeyPairId": "key-0bac06a768f60a783",
                    "KeyType": "ed25519",
                    "Tags": [
                        {
                            "Key": "Name",
                            "Value": "ec2 key pair"
                        }
                    ],
                    "CreateTime": "2024-10-22T03:27:49.685000+00:00",
                    "KeyName": "ec2_key",
                    "KeyFingerprint": "zpne2qe0PsuUoswSE8lRO2I6hYe+FxVC35ndxnhi/yU="
                }
            ]
        }
        ```
- Querying only the specific fields using --query flag from describe output
    - `aws ec2 describe-key-pairs --query 'KeyPairs[].KeyName'`   
    Output
        ```
        [
            "jenkins_ec2",
            "ec2_key"
        ]
        ```

## create-key-pair
