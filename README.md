# Overview
During an assessment of the application’s internal routing and request handling, I identified a high-severity Server-Side Request Forgery (SSRF) vulnerability caused by trusting user-supplied Host headers. By manipulating this header, it was possible to route requests to internal services within the 192.168.0.0/24 subnet, ultimately granting access to an internal admin panel. This allowed unauthorized actions such as deleting a user account.

# Methodology

Step 1: Intercepted and analyzed HTTP requests using Burp Suite to understand routing behavior.

Step 2: Tested network interactions using Burp Collaborator to confirm the server processes external requests based on the Host header.

Step 3: Performed iterative Host header modifications to scan internal IP addresses (192.168.0.0/24) and locate the internal admin panel.

Step 4: Accessed the /admin panel internally and extracted CSRF tokens and session cookies from the responses.

Step 5: Crafted POST requests to perform privileged actions, including deleting a user, successfully confirming exploitation.

# Conclusion

This assessment confirmed a critical SSRF vulnerability via routing decisions based on the Host header. Exploitation allowed unauthorized access to internal administrative interfaces and sensitive operations. Mitigation requires removing trust in client-controlled headers, enforcing network segmentation, and applying authentication and CSRF protections to all internal endpoints.
