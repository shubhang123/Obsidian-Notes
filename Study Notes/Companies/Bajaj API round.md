Here’s a clear breakdown of how to solve the **Bajaj Finserv Programming Challenge** using Python:

---

### ✅ **Step-by-Step Approach**

---

### 🔹 **Step 1: GET Request**

Send a `GET` request with your registered mobile number to retrieve:

- A list of numbers `Y`
    
- A secret key `x`
    

**Endpoint:**

```
GET https://bfhldevapigw.healthrx.co.in/campus-hiring/input?id=YourMobileNumber
```

---

### 🔹 **Step 2: Compute Statistics**

Given the list `Y`, calculate:

- Count
    
- Minimum
    
- Maximum
    
- Mean (rounded to 2 decimal places)
    
- Median
    
- Mode (if multiple modes, use the smallest)
    

---

### 🔹 **Step 3: POST Request**

Send a `POST` request with all the computed values and the secret.

**Endpoint:**

```
POST https://bfhldevapigw.healthrx.co.in/campus-hiring/submit?id=YourMobileNumber
```

**Headers:**

```json
{
  "Content-Type": "application/json"
}
```

**Payload Format:**

```json
{
  "Size": ...,
  "Mean": ...,
  "Median": ...,
  "Mode": ...,
  "Min": ...,
  "Max": ...,
  "Secret": "..."
}
```

---

### 🧠 Sample Python Code

```python
import requests
import statistics as stats

# Step 1: Replace with your actual registered mobile number
mobile_number = "9876543210"
get_url = f"https://bfhldevapigw.healthrx.co.in/campus-hiring/input?id={mobile_number}"

# Send GET request
response = requests.get(get_url)
data = response.json()

# Parse response
Y = eval(data["Data"])  # Convert string list to actual list
secret = data["Secret"]

# Step 2: Calculate required statistics
count = len(Y)
_min = min(Y)
_max = max(Y)
_mean = round(sum(Y) / count, 2)
_median = int(stats.median(Y))  # as per API docs, keep it int
_mode = int(min(stats.multimode(Y)))  # smallest mode if multiple

# Step 3: Send POST request
post_url = f"https://bfhldevapigw.healthrx.co.in/campus-hiring/submit?id={mobile_number}"
headers = {
    "Content-Type": "application/json"
}

payload = {
    "Size": count,
    "Mean": _mean,
    "Median": _median,
    "Mode": _mode,
    "Min": _min,
    "Max": _max,
    "Secret": secret
}

post_response = requests.post(post_url, json=payload, headers=headers)

# Final output
print(post_response.text)
```

---

### 🔒 Notes:

- **Don't exceed 10 API attempts.**
    
- **Your last correct POST is final.**
    
- **Round mean to two decimal places.**
    
- Ensure data types match: Mean can be float, rest should be int.
    

---

Would you like me to run a test using dummy data to show you sample output?