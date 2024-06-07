---
id: 20240607110900
tags: [python, django]
---

# Reversing Admin URLs in Django

<https://en.proft.me/2014/10/12/reversing-admin-urls-django/>

| Action     | Pattern                                       | Args        |
| ---------- | --------------------------------------------- | ----------- |
| Changelist | `{{ app_label }}_{{ model_name }}_changelist` |             |
| Add        | `{{ app_label }}_{{ model_name }}_add`        |             |
| History    | `{{ app_label }}_{{ model_name }}_history`    | `object_id` |
| Delete     | `{{ app_label }}_{{ model_name }}_delete`     | `object_id` |
| Change     | `{{ app_label }}_{{ model_name }}_change`     | `object_id` |

### Example
For the `change` view for an object (Model) `User` from the `user` app:

```python
from django.urls import reverse

reverse("admin:user_user_change", kwargs={"object_id": 1})
```

Replace `object_id` with the name of the captured value that is expected

Related:
