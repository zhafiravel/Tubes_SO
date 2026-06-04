\# 1. Backup konfigurasi SSH asli

sudo cp /etc/ssh/sshd\_config /etc/ssh/sshd\_config.backup

\# 2. Edit file konfigurasi SSH

sudo nano /etc/ssh/sshd\_config

\# 3. Ubah parameter berikut:

\# Port 2222

\# PermitRootLogin no

\# PubkeyAuthentication yes

\# PasswordAuthentication no (opsional, jika key sudah disetting)

\# MaxAuthTries 3

\# AllowUsers ubuntu

\# 4. Buka port baru pada firewall

sudo ufw allow 2222/tcp

sudo ufw delete allow 22/tcp # tutup port 22 setelah diuji

sudo ufw enable

sudo ufw reload

\# 5. Restart layanan SSH

sudo systemctl restart ssh

\# atau pada beberapa distro:

sudo systemctl restart sshd

\# 6. (PENTING) Update Network Security Group di Azure:

\# - Tambahkan inbound rule untuk port 2222/tcp

\# - Hapus inbound rule untuk port 22/tcp

\# 7. Uji koneksi dari laptop lokal

ssh -p 2222 ubuntu@<IP\_PUBLIC\_VM>

