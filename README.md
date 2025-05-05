# Backup
# Velero + MinIO Setup

1. Install Velero CLI → `wget`, `tar`, `mv` to `/usr/local/bin/`.  
2. Add `192.168.61.93 minio.toucanint.com` to `/etc/hosts` on all nodes.  
3. Create `credentials-velero` with MinIO creds (`minioadmin`).  
4. Install with: `velero install --provider aws --bucket work-test --secret-file ./credentials-velero --plugins velero/velero-plugin-for-aws:v1.2.1 --use-volume-snapshots=false --backup-location-config region=minio,s3ForcePathStyle=true,s3Url=https://minio.toucanint.com,publicUrl=https://minio.toucanint.com --namespace velero`.  
5. Backup: `velero create backup <name>` | Restore: `velero restore create <name> --from-backup <backup>`.  
6. Check DNS: `kubectl run dns-test --rm -it --image=busybox --restart=Never -- sh -c 'nslookup minio.toucanint.com'`.  
