kibana 5.6.11 remove x-pack plugin
kibana.yml config needs add:
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Chart.Name }}-config-{{ .Release.Name }}
data:
  kibana.yml: |
    server.port: 5601
    server.host: "0.0.0.0"
    {{- if .Values.elasticsearch.enable}}
    elasticsearch.url: "http://{{ .Release.Name }}-elasticsearch:9200"
    {{- else }}
    elasticsearch.url: {{ .Values.elasticsearch.url}}
    {{- end }}
    elasticsearch.requestTimeout: 90000
    xpack.ml.enabled: false
    xpack.monitoring.enabled: false
    xpack.reporting.enabled: false
    xpack.security.enabled: false
    xpack.graph.enabled: false
