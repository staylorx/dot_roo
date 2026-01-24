# Debug

When debugging for webapps, specifically Flutter, create a browser with a web-port for checking navigation and other app behavior:

```bash
flutter run -d web-server --web-port=8080
```

Then use the playwrite MCP to work on the app in the browser. Certain systems won't be available, specifically some databases, camera, and other IO. Still, do what you can with what you have.

If you find yourself needing the user to copy debug, stacktraces, or errors, run the app yourself to determine what issues might be causing problems.
