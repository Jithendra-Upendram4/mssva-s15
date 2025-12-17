Required Details:

Challenge ID: CH2  
Target URL: http://127.0.0.1:8002/download?file=secret.txt  
Finding Summary: Path traversal vulnerability with NO authentication/authorization. Created a file (secret.txt) in /tmp/files directory and accessed it via browser without any auth. The endpoint has no path traversal protection allowing LFI attacks to read sensitive files like /etc/passwd (Linux) or win.ini (Windows). Also responds with "Not found" (404) for missing files and "Not allowed" (403) when traversal is blocked.  
Detection Method: Custom Nuclei template  
Template File: ch2-file-traversal.yaml
