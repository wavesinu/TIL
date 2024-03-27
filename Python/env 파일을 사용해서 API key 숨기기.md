```python
# Bad code
API_KEY = "3ebf52c0-3ebf52c0"
response = requests.get(f"https://example.com/api/?api_key={API_KEY}")
```

```python
import os
from dotenv import load_dotenv
load_dotenv()

API_KEY = os.getenv('PROJECT_API_KEY')
```

