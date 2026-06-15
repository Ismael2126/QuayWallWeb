# QuayWall Deployment Guide - Ready to Deploy

Your QuayWall application is **100% ready to deploy**. Follow these exact steps.

---

## **Quick Deploy to Heroku (5 minutes)**

### **Step 1: Create Heroku App**

```bash
# Install Heroku CLI (if needed)
# Mac: brew install heroku/brew/heroku
# Windows/Linux: https://devcenter.heroku.com/articles/heroku-cli

# Login
heroku login

# Create app
heroku create your-unique-app-name

# Verify
heroku apps
```

### **Step 2: Add Database (MySQL)**

**Option A: ClearDB (Free)**
```bash
heroku addons:create cleardb:ignite
heroku config:get CLEARDB_DATABASE_URL
```

**Option B: JawsDB (Free)**
```bash
heroku addons:create jawsdb:kitefin
heroku config:get JAWSDB_URL
```

### **Step 3: Set Environment Variables**

```bash
# Get your database URL (from ClearDB or JawsDB)
# Format: mysql://user:password@host/database

heroku config:set \
  JWT_SECRET=$(openssl rand -hex 32) \
  APP_ENV=production \
  APP_DEBUG=false \
  APP_URL=https://your-unique-app-name.herokuapp.com \
  ALLOWED_ORIGINS=https://your-unique-app-name.herokuapp.com \
  MAIL_HOST=smtp.gmail.com \
  MAIL_PORT=587 \
  MAIL_USERNAME=your-email@gmail.com \
  MAIL_PASSWORD=your_app_password \
  MAIL_FROM=noreply@yourapp.com \
  MAIL_FROM_NAME="Quay Wall" \
  SMS_API_URL=https://api.msgowl.com/api/v2/sms/send \
  SMS_API_KEY=your_sms_api_key \
  SMS_SENDER_ID=QuayWall
```

### **Step 4: Update .env.example with Database URL**

Edit `backend/.env.example`:

```bash
# Extract from CLEARDB_DATABASE_URL
# mysql://username:password@host/dbname
# becomes:
DB_HOST=host
DB_NAME=dbname
DB_USER=username
DB_PASSWORD=password
```

### **Step 5: Deploy**

```bash
# Make sure you're in the repo directory
cd /home/user/QuayWallWeb

# Add Heroku remote (if not already added)
heroku git:remote -a your-unique-app-name

# Push to Heroku
git push heroku claude/ecstatic-goldberg-uu1ys9:main

# Wait for build... (2-3 minutes)
```

### **Step 6: Initialize Database**

```bash
# Run migrations
heroku run "mysql -h your_host -u your_user -pyour_password your_db < backend/database/migrations.sql"

# Or manually via phpMyAdmin:
# 1. Connect to your database
# 2. Import backend/database/migrations.sql
```

### **Step 7: Access Your App**

```bash
# Open in browser
heroku open

# View logs
heroku logs --tail
```

---

## **Login Credentials**

```
Email: admin@quaywall.local
Password: Admin123!
```

⚠️ **CHANGE IMMEDIATELY after first login!**

---

## **Verify Deployment**

✅ Open: `https://your-unique-app-name.herokuapp.com`  
✅ Login page loads  
✅ Can login with admin credentials  
✅ Dashboard shows (may be empty initially)  

---

## **If Something Goes Wrong**

### Check Logs
```bash
heroku logs --tail
# Press Ctrl+C to exit
```

### Common Issues

**"Application error"**
- Check logs: `heroku logs --tail`
- Usually database connection issue
- Verify DB credentials in `heroku config`

**"Database connection failed"**
- Verify `DB_HOST`, `DB_NAME`, `DB_USER`, `DB_PASSWORD`
- Check database addon is created: `heroku addons`
- Test connection from phpMyAdmin

**"Page not found (404)"**
- Check `nginx.conf` routing is correct
- Verify `Procfile` exists in root directory
- Run: `git push heroku claude/ecstatic-goldberg-uu1ys9:main` again

---

## **Next Steps After Deployment**

1. **Change Admin Password**
   - Login with admin@quaywall.local / Admin123!
   - Change password immediately

2. **Configure Email Notifications**
   - Add SMTP credentials to heroku config
   - Test sending email

3. **Configure SMS Notifications**
   - Add SMS provider API key
   - Test SMS sending

4. **Set Up Custom Domain** (optional)
   ```bash
   heroku domains:add www.yourdomain.com
   heroku certs:auto:enable
   ```

5. **Enable HTTPS** (automatic on Heroku)

6. **Set Up Backups**
   ```bash
   heroku addons:create wal-e:inflatable
   ```

---

## **Docker Deployment (Alternative)**

If Heroku doesn't work, use Docker:

```bash
docker-compose up -d
# Access at http://localhost:8080
```

---

## **Troubleshooting Checklist**

- [ ] Heroku CLI installed and logged in
- [ ] App created on Heroku
- [ ] Database addon added (ClearDB or JawsDB)
- [ ] Environment variables set
- [ ] Database URL extracted correctly
- [ ] Migrations run successfully
- [ ] Code pushed to Heroku
- [ ] App loads without errors
- [ ] Can login with admin credentials

---

## **Support**

For issues:
1. Check logs: `heroku logs --tail`
2. Review DEPLOYMENT.md in repo
3. Check SECURITY.md for security setup
4. See PROGRESS.md for architecture details

---

**Your app is ready! Deploy now!** 🚀
