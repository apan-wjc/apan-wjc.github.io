### calendar
```python
python3 -m calendar 2026
```
### this
```python
python3 -c "import this"
```
### http server
```python
python3 -m http.server 8000 --bind 0.0.0.0
```
### pretty-print JSON
```python
echo '{"name":"Alice","age":30}' | python3 -m json.tool
```
### validate a JSON
```python
python3 -m json.tool data.json
```
### list installed
```python
python3 -c "help('modules')"
```
### password gen 
```python
python3 -c "import secrets,string;print(''.join(secrets.choice(string.ascii_letters+string.digits) for _ in range(32)))"
```
### password gen with special chars
```python
python3 -c "import secrets,string;print(''.join(secrets.choice(string.ascii_letters+string.digits+string.punctuation) for _ in range(32)))"
```
### get public IP
```python
python3 -c "import urllib.request; print(urllib.request.urlopen('https://api.ipify.org').read().decode())"
```
