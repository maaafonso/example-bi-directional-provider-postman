#!/bin/bash

SUCCESS=true
if [ "${1}" != "true" ]; then
  SUCCESS=false
fi
OAS=$(cat oas/swagger.yml | base64) # Pass the "-w 0" flag if on linux
#REPORT=$(cat /path/to/report.file | base64)

echo "==> Uploading OAS to Pactflow"
curl \
  -X PUT \
  -H "Authorization: Bearer ${PACT_BROKER_TOKEN}" \
  -H "Content-Type: application/json" \
  "${PACT_BROKER_BASE_URL}/contracts/provider/${PACTICIPANT}/version/${GIT_COMMIT}" \
  -d '{
   "content": "'$OAS'",
   "contractType": "oas",
   "contentType": "application/yaml",
   "verificationResults": {
     "success": '$SUCCESS',
     "contentType": "text/plain",
     "verifier": "verifier"
   }
 }'