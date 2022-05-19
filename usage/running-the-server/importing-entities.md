---
description: How to batch-import organizations, users, collaborations, etc.
---

# Batch import

{% hint style="danger" %}
All users that are imported using `vserver import` receive the superuser role. We are looking into ways to also be able to import roles. For more background info refer to this [issue](https://github.com/IKNL/vantage6-server/issues/12).
{% endhint %}

To batch import users, organizations and collaborations you can use the `vserver import /path/to/file.yaml` command. The `yaml` file is expected to have the following format:

{% code title="example_fixtures.yaml" %}
```yaml
organizations:

  - name:       IKNL
    domain:     iknl.nl
    address1:   Godebaldkwartier 419
    address2:
    zipcode:    3511DT
    country:    Netherlands
    users:
      - username: admin
        firstname: admin
        lastname: robot
        password: password
      - username: frank@iknl.nl
        firstname: Frank
        lastname: Martin
        password: password
      - username: melle@iknl.nl
        firstname: Melle
        lastname: Sieswerda
        password: password
    public_key: LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0KTUlJQ0lqQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FnOEFNSUlDQ2dLQ0FnRUF2eU4wWVZhWWVZcHVWRVlpaDJjeQphTjdxQndCUnB5bVVibnRQNmw2Vk9OOGE1eGwxMmJPTlQyQ1hwSEVGUFhZQTFFZThQRFZwYnNQcVVKbUlseWpRCkgyN0NhZTlIL2lJbUNVNnViUXlnTzFsbG1KRTJQWDlTNXVxendVV3BXMmRxRGZFSHJLZTErUUlDRGtGSldmSEIKWkJkczRXMTBsMWlxK252dkZ4OWY3dk8xRWlLcVcvTGhQUS83Mm52YlZLMG9nRFNaUy9Jc1NnUlk5ZnJVU1FZUApFbGVZWUgwYmI5VUdlNUlYSHRMQjBkdVBjZUV4dXkzRFF5bXh2WTg3bTlkelJsN1NqaFBqWEszdUplSDAwSndjCk80TzJ0WDVod0lLL1hEQ3h4eCt4b3cxSDdqUWdXQ0FybHpodmdzUkdYUC9wQzEvL1hXaVZSbTJWZ3ZqaXNNaisKS2VTNWNaWWpkUkMvWkRNRW1QU29rS2Y4UnBZUk1lZk0xMWtETTVmaWZIQTlPcmY2UXEyTS9SMy90Mk92VDRlRgorUzVJeTd1QWk1N0ROUkFhejVWRHNZbFFxTU5QcUpKYlRtcGlYRWFpUHVLQitZVEdDSC90TXlrRG1JK1dpejNRCjh6SVo1bk1IUnhySFNqSWdWSFdwYnZlTnVaL1Q1aE95aE1uZHU0c3NpRkJyUXN5ZGc1RlVxR3lkdE1JMFJEVHcKSDVBc1ovaFlLeHdiUm1xTXhNcjFMaDFBaDB5SUlsZDZKREY5MkF1UlNTeDl0djNaVWRndEp5VVlYN29VZS9GKwpoUHVwVU4rdWVTUndGQjBiVTYwRXZQWTdVU2RIR1diVVIrRDRzTVQ4Wjk0UVl2S2ZCanU3ZXVKWSs0Mmd2Wm9jCitEWU9ZS05qNXFER2V5azErOE9aTXZNQ0F3RUFBUT09Ci0tLS0tRU5EIFBVQkxJQyBLRVktLS0tLQo=

  - name:       Small Organization
    domain:     small-organization.example
    address1:   Big Ambitions Drive 4
    address2:
    zipcode:    1234AB
    country:    Nowhereland
    users:
      - username: admin@small-organization.example
        firstname: admin
        lastname: robot
        password: password
      - username: stan
        firstname: Stan
        lastname: the man
        password: password
    public_key: LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0KTUlJQ0lqQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FnOEFNSUlDQ2dLQ0FnRUF2eU4wWVZhWWVZcHVWRVlpaDJjeQphTjdxQndCUnB5bVVibnRQNmw2Vk9OOGE1eGwxMmJPTlQyQ1hwSEVGUFhZQTFFZThQRFZwYnNQcVVKbUlseWpRCkgyN0NhZTlIL2lJbUNVNnViUXlnTzFsbG1KRTJQWDlTNXVxendVV3BXMmRxRGZFSHJLZTErUUlDRGtGSldmSEIKWkJkczRXMTBsMWlxK252dkZ4OWY3dk8xRWlLcVcvTGhQUS83Mm52YlZLMG9nRFNaUy9Jc1NnUlk5ZnJVU1FZUApFbGVZWUgwYmI5VUdlNUlYSHRMQjBkdVBjZUV4dXkzRFF5bXh2WTg3bTlkelJsN1NqaFBqWEszdUplSDAwSndjCk80TzJ0WDVod0lLL1hEQ3h4eCt4b3cxSDdqUWdXQ0FybHpodmdzUkdYUC9wQzEvL1hXaVZSbTJWZ3ZqaXNNaisKS2VTNWNaWWpkUkMvWkRNRW1QU29rS2Y4UnBZUk1lZk0xMWtETTVmaWZIQTlPcmY2UXEyTS9SMy90Mk92VDRlRgorUzVJeTd1QWk1N0ROUkFhejVWRHNZbFFxTU5QcUpKYlRtcGlYRWFpUHVLQitZVEdDSC90TXlrRG1JK1dpejNRCjh6SVo1bk1IUnhySFNqSWdWSFdwYnZlTnVaL1Q1aE95aE1uZHU0c3NpRkJyUXN5ZGc1RlVxR3lkdE1JMFJEVHcKSDVBc1ovaFlLeHdiUm1xTXhNcjFMaDFBaDB5SUlsZDZKREY5MkF1UlNTeDl0djNaVWRndEp5VVlYN29VZS9GKwpoUHVwVU4rdWVTUndGQjBiVTYwRXZQWTdVU2RIR1diVVIrRDRzTVQ4Wjk0UVl2S2ZCanU3ZXVKWSs0Mmd2Wm9jCitEWU9ZS05qNXFER2V5azErOE9aTXZNQ0F3RUFBUT09Ci0tLS0tRU5EIFBVQkxJQyBLRVktLS0tLQo=

  - name:       Big Organization
    domain:     big-organization.example
    address1:   Offshore Accounting Drive 19
    address2:
    zipcode:    54331
    country:    Nowhereland
    users:
      - username: admin@big-organization.example
        firstname: admin
        lastname: robot
        password: password
    public_key: LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0KTUlJQ0lqQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FnOEFNSUlDQ2dLQ0FnRUF2eU4wWVZhWWVZcHVWRVlpaDJjeQphTjdxQndCUnB5bVVibnRQNmw2Vk9OOGE1eGwxMmJPTlQyQ1hwSEVGUFhZQTFFZThQRFZwYnNQcVVKbUlseWpRCkgyN0NhZTlIL2lJbUNVNnViUXlnTzFsbG1KRTJQWDlTNXVxendVV3BXMmRxRGZFSHJLZTErUUlDRGtGSldmSEIKWkJkczRXMTBsMWlxK252dkZ4OWY3dk8xRWlLcVcvTGhQUS83Mm52YlZLMG9nRFNaUy9Jc1NnUlk5ZnJVU1FZUApFbGVZWUgwYmI5VUdlNUlYSHRMQjBkdVBjZUV4dXkzRFF5bXh2WTg3bTlkelJsN1NqaFBqWEszdUplSDAwSndjCk80TzJ0WDVod0lLL1hEQ3h4eCt4b3cxSDdqUWdXQ0FybHpodmdzUkdYUC9wQzEvL1hXaVZSbTJWZ3ZqaXNNaisKS2VTNWNaWWpkUkMvWkRNRW1QU29rS2Y4UnBZUk1lZk0xMWtETTVmaWZIQTlPcmY2UXEyTS9SMy90Mk92VDRlRgorUzVJeTd1QWk1N0ROUkFhejVWRHNZbFFxTU5QcUpKYlRtcGlYRWFpUHVLQitZVEdDSC90TXlrRG1JK1dpejNRCjh6SVo1bk1IUnhySFNqSWdWSFdwYnZlTnVaL1Q1aE95aE1uZHU0c3NpRkJyUXN5ZGc1RlVxR3lkdE1JMFJEVHcKSDVBc1ovaFlLeHdiUm1xTXhNcjFMaDFBaDB5SUlsZDZKREY5MkF1UlNTeDl0djNaVWRndEp5VVlYN29VZS9GKwpoUHVwVU4rdWVTUndGQjBiVTYwRXZQWTdVU2RIR1diVVIrRDRzTVQ4Wjk0UVl2S2ZCanU3ZXVKWSs0Mmd2Wm9jCitEWU9ZS05qNXFER2V5azErOE9aTXZNQ0F3RUFBUT09Ci0tLS0tRU5EIFBVQkxJQyBLRVktLS0tLQo=

collaborations:

  - name: ZEPPELIN
    participants:
      - IKNL
      - Small Organization
      - Big Organization
    tasks: ["hello-world"]
    encrypted: false

  - name: PIPELINE
    participants:
      - IKNL
      - Big Organization
    tasks: ["hello-world"]
    encrypted: false

  - name: SLIPPERS
    participants:
      - Small Organization
      - Big Organization
    tasks: ["hello-world", "hello-world"]
    encrypted: false
```
{% endcode %}
