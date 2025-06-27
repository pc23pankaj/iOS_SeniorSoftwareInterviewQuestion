Sure! Here's a **standard Swift example** of making an API call using:

* A **protocol** for API service
* A **generic method** for decoding any `Codable` model
* A **model struct** conforming to `Codable`
* A **completion handler** with success and failure responses

---

### Step 1: Define the Model

```swift
struct User: Codable {
    let id: Int
    let name: String
    let email: String
}
```

---

### Step 2: Define API Service Protocol

```swift
protocol APIServiceProtocol {
    func fetchData<T: Codable>(from urlString: String, completion: @escaping (Result<T, Error>) -> Void)
}
```

---

### Step 3: Create API Service Implementation

```swift
import Foundation

class APIService: APIServiceProtocol {
    
    func fetchData<T: Codable>(from urlString: String, completion: @escaping (Result<T, Error>) -> Void) {
        
        // 1. Validate URL
        guard let url = URL(string: urlString) else {
            completion(.failure(APIError.invalidURL))
            return
        }
        
        // 2. Create URLSession data task
        URLSession.shared.dataTask(with: url) { data, response, error in
            
            // 3. Handle error from the network call
            if let error = error {
                completion(.failure(error))
                return
            }
            
            // 4. Validate response and data
            guard let httpResponse = response as? HTTPURLResponse,
                  200..<300 ~= httpResponse.statusCode else {
                completion(.failure(APIError.invalidResponse))
                return
            }
            
            guard let data = data else {
                completion(.failure(APIError.noData))
                return
            }
            
            // 5. Decode data into the generic Codable model T
            do {
                let decodedObject = try JSONDecoder().decode(T.self, from: data)
                completion(.success(decodedObject))
            } catch {
                completion(.failure(error))
            }
            
        }.resume()
    }
}

// Custom API Errors
enum APIError: Error {
    case invalidURL
    case invalidResponse
    case noData
}
```

---

### Step 4: Usage Example

```swift
let apiService = APIService()
let userAPI = "https://jsonplaceholder.typicode.com/users/1"

apiService.fetchData(from: userAPI) { (result: Result<User, Error>) in
    switch result {
    case .success(let user):
        print("User name: \(user.name), email: \(user.email)")
    case .failure(let error):
        print("Error: \(error.localizedDescription)")
    }
}
```

---

### Explanation:

* The protocol `APIServiceProtocol` declares a generic `fetchData` function.
* The `APIService` class implements the protocol and handles network request, error handling, and JSON decoding.
* The completion handler uses `Result<T, Error>` for better error handling.
* The model `User` conforms to `Codable`.
* You can use this service to fetch any Codable model by specifying the type in the completion handler.

---
