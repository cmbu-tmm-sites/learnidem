---
title: "Present Update"
weight: 25
---

New Idem state feature: <b>force_update</b> are supported on most resources. This flag is default to “False”.<br>
If the flag is set to “True” in an SLS file, the resource will be updated via “PUT” operation. This will allow parameters that aren’t supported in the “PATCH” operation to be updated.

