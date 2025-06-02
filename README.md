
<body>

  <h1>README.md</h1>
  <p>
    This document provides the minimal information needed to interact with the 
    <code>https://kindergarten2.istream.uz/customer/token</code> endpoint. By sending 
    a <strong>POST</strong> request to this endpoint, you can obtain an 
    <code>access_token</code>.
  </p>

  <h2>1. Endpoint</h2>
  <p>
    <strong>URL:</strong> <code>https://kindergarten2.istream.uz/customer/token</code><br />
    <strong>HTTP Method:</strong> <code>POST</code>
  </p>

  <h2>2. Required Headers</h2>
  <p>When sending the request, include the following HTTP headers:</p>
  <table>
    <thead>
      <tr>
        <th>Header Name</th>
        <th>Value / Example</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>Content-Type</code></td>
        <td><code>application/x-www-form-urlencoded</code></td>
        <td>Indicates form data is being sent</td>
      </tr>
      <tr>
        <td><code>integrity-token</code></td>
        <td><code>{YOUR_INTEGRITY_TOKEN}</code></td>
        <td>
          A pre-shared JWT or encryption token for authorization. Example:
          <br />
          <span style="word-break: break-all;">
            <code>
eyJhbGciOiJBMjU2S1ciLCJlbmMiOiJBMjU2R0NNIn0.wKD7hvqtiabejfWtYzVO9Syn5G22sLHT...
            </code>
          </span>
        </td>
      </tr>
      <tr>
        <td><code>X-App-Source</code></td>
        <td><code>PlayMarket</code></td>
        <td>Indicates the app source (always “PlayMarket”)</td>
      </tr>
      <tr>
        <td><code>App-Version-Code</code></td>
        <td><code>1.3.2-pm</code></td>
        <td>The application version code</td>
      </tr>
      <tr>
        <td><code>App-Version-Name</code></td>
        <td><code>1.3.2-pm</code></td>
        <td>The application version name</td>
      </tr>
      <tr>
        <td><code>Device-Id</code></td>
        <td><code>{RANDOM_UUID}</code></td>
        <td>
          A unique device identifier (UUID) generated per request.<br />
          Example: <code>550e8400-e29b-41d4-a716-446655440000</code>
        </td>
      </tr>
      <tr>
        <td><code>Device-Name</code></td>
        <td><code>Xiaomi M2101K7AG</code></td>
        <td>The full device name (brand + model)</td>
      </tr>
      <tr>
        <td><code>Device-Manufacturer</code></td>
        <td><code>Xiaomi</code></td>
        <td>The device manufacturer (brand)</td>
      </tr>
      <tr>
        <td><code>Device-Model</code></td>
        <td><code>M2101K7AG</code></td>
        <td>The device model</td>
      </tr>
      <tr>
        <td><code>Android-OS</code></td>
        <td><code>34</code></td>
        <td>The Android OS version</td>
      </tr>
      <tr>
        <td><code>Accept-Language</code></td>
        <td><code>uz</code></td>
        <td>Preferred response language (uz = Uzbek)</td>
      </tr>
      <tr>
        <td><code>User-Agent</code></td>
        <td><code>okhttp/4.9.3</code></td>
        <td>The HTTP client User-Agent string</td>
      </tr>
    </tbody>
  </table>

  <h2>3. Request Body</h2>
  <p>
    Send the following form fields in <code>application/x-www-form-urlencoded</code> format:
  </p>
  <table>
    <thead>
      <tr>
        <th>Field Name</th>
        <th>Value / Example</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>username</code></td>
        <td><code>SEVARA_199595</code></td>
        <td>The MTT user’s login name</td>
      </tr>
      <tr>
        <td><code>password</code></td>
        <td><code>sevara</code></td>
        <td>The MTT user’s password</td>
      </tr>
    </tbody>
  </table>

  <h2>4. Response</h2>
  <p>If the request is valid, the server returns HTTP <code>200 OK</code> with JSON:</p>
  <pre><code>{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
  </code></pre>
  <p>If credentials are invalid or another error occurs, the server returns a <code>4xx</code> or <code>5xx</code> status, for example:</p>
  <pre><code>{
  "detail": "Invalid credentials"
}
  </code></pre>

  <h2>5. Example (curl)</h2>
  <p>Example using <code>curl</code>:</p>
  <pre><code>curl -X POST "https://kindergarten2.istream.uz/customer/token" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "integrity-token: eyJhbGciOiJBMjU2S1ciLCJlbmMiOiJBMjU2R0NNIn0.wKD7hvqtiabejfWtYzVO9Syn5G22sLHT..." \
  -H "X-App-Source: PlayMarket" \
  -H "App-Version-Code: 1.3.2-pm" \
  -H "App-Version-Name: 1.3.2-pm" \
  -H "Device-Id: 550e8400-e29b-41d4-a716-446655440000" \
  -H "Device-Name: Xiaomi M2101K7AG" \
  -H "Device-Manufacturer: Xiaomi" \
  -H "Device-Model: M2101K7AG" \
  -H "Android-OS: 34" \
  -H "Accept-Language: uz" \
  -H "User-Agent: okhttp/4.9.3" \
  -d "username=SEVARA_199595" \
  -d "password=sevara"
  </code></pre>

  <h2>6. Notes</h2>
  <ul>
    <li>
      <strong>integrity-token</strong> must be a valid pre-shared JWT or encryption token.
      If it’s expired or incorrect, the request will be rejected.
    </li>
    <li>
      <strong>Device-Id</strong> should be a unique UUID generated for each request.
      In Python: <code>str(uuid.uuid4())</code>.
    </li>
    <li>
      After a successful request, store the returned <code>access_token</code> 
      for subsequent authenticated API calls.
    </li>
    <li>
      If the server returns an error JSON, check the <code>detail</code> or 
      <code>error</code> field for more information.
    </li>
  </ul>

  <h2>7. How to Use (Python Example)</h2>
  <p>You can use this code snippet in a Django view or standalone Python script:</p>
  <pre><code>import requests
import uuid

INTEGRITY_TOKEN = (
  "eyJhbGciOiJBMjU2S1ciLCJlbmMiOiJBMjU2R0NNIn0.wKD7hvqtiabejfWt... (full token here)"
)

def get_access_token(username: str, password: str):
    url = "https://kindergarten2.istream.uz/customer/token"
    data = {
        "username": username.strip(),
        "password": password.strip()
    }
    headers = {
        "Content-Type": "application/x-www-form-urlencoded",
        "integrity-token": INTEGRITY_TOKEN,
        "X-App-Source": "PlayMarket",
        "App-Version-Code": "1.3.2-pm",
        "App-Version-Name": "1.3.2-pm",
        "Device-Id": str(uuid.uuid4()),
        "Device-Name": "Xiaomi M2101K7AG",
        "Device-Manufacturer": "Xiaomi",
        "Device-Model": "M2101K7AG",
        "Android-OS": "34",
        "Accept-Language": "uz",
        "User-Agent": "okhttp/4.9.3"
    }

    session = requests.Session()
    session.trust_env = False
    session.proxies = {"http": None, "https": None}

    try:
        response = session.post(url, data=data, headers=headers, timeout=10)
    except requests.RequestException as e:
        print("Requests error:", e)
        return None

    if response.status_code != 200:
        print("HTTP error code:", response.status_code)
        print("Server response:", response.text)
        return None

    try:
        token_json = response.json()
    except ValueError:
        print("JSON decode error:", response.text)
        return None

    return token_json.get("access_token")

if __name__ == "__main__":
    user = "SEVARA_199595"
    pwd = "sevara"
    token = get_access_token(user, pwd)
    print("Retrieved token:", token)
</code></pre>

  <h2>8. Summary</h2>
  <p>
    This README.md provides the necessary details for sending a <code>POST</code> 
    request to the <code>/customer/token</code> endpoint, including required headers, 
    request body fields, and expected JSON response. Publish this document publicly 
    (e.g., on GitHub) and include the link when requesting whitelist approval 
    from PythonAnywhere.
  </p>

</body>
</html>
