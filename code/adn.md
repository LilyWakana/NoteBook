```
import (
	"encoding/json"
	"net/http"
)

func WriteResponseJSON(w http.ResponseWriter, v interface{}) {
	w.Header()["Content-Type"] = jsonContentType
	enc := json.NewEncoder(w)
	enc.SetEscapeHTML(false)
	err := enc.Encode(v)
	if err != nil {
		http.Error(w, err.Error(), http.StatusInternalServerError)
	}
}

```
