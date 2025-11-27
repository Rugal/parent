# Migration to Maven Central Publisher Portal

This document describes how to migrate from OSSRH to the new Maven Central Publisher Portal.

## What Changed

As of June 30, 2025, OSSRH (oss.sonatype.org) has been deprecated and replaced by the Central Publisher Portal at https://central.sonatype.com/

## Migration Steps

### 1. Setup Central Portal Account

1. Go to https://central.sonatype.com/
2. Log in with your existing OSSRH credentials
3. Navigate to **"Namespaces"** section
4. If your namespace `ga.rugal` is not listed, use the **"Migrate Namespace"** option
5. Go to **"Account"** → **"Generate User Token"**
   - This will generate a username/password pair
   - Save these credentials securely

### 2. Update Maven Settings

Update your `~/.m2/settings.xml` file with the new credentials:

```xml
<settings>
  <servers>
    <server>
      <id>central</id>
      <username>YOUR_USER_TOKEN_USERNAME</username>
      <password>YOUR_USER_TOKEN_PASSWORD</password>
    </server>
  </servers>
</settings>
```

**Important Notes:**
- Replace `YOUR_USER_TOKEN_USERNAME` and `YOUR_USER_TOKEN_PASSWORD` with the token you generated
- The server `<id>` must be `central` to match the distributionManagement configuration
- Consider encrypting your passwords using Maven's password encryption feature

### 3. POM.xml Changes (Already Applied)

The following changes have been made to your `pom.xml`:

1. **Repository URLs** updated from OSSRH to Central Portal:
   - Old: `https://oss.sonatype.org/...`
   - New: `https://central.sonatype.com/api/v1/publisher`

2. **Distribution Management** - server ID changed from `ossrh` to `central`

3. **Nexus Staging Plugin** - Removed (no longer needed)
   - The new Central Portal uses direct deployment via `maven-deploy-plugin`

4. **Profile** - Added new `central` profile

### 4. Publishing Process

#### Option A: Direct Deployment with Publishing

```bash
# Build and deploy (with GPG signing)
mvn clean deploy -Pcentral

# Or with the legacy profile name
mvn clean deploy -Psonatype
```

#### Option B: Using Maven Release Plugin

```bash
# Prepare and perform release
mvn release:prepare release:perform -Pcentral
```

### 5. Verify Deployment

1. Log in to https://central.sonatype.com/
2. Navigate to **"Deployments"** section
3. Review your uploaded artifacts
4. Click **"Publish"** to release to Maven Central

## Important Notes

### Artifact Requirements

All artifacts must still meet Maven Central requirements:
- ✅ GPG signed (`.asc` files)
- ✅ Javadoc JAR
- ✅ Sources JAR
- ✅ POM with required metadata:
  - name, description, url
  - licenses
  - developers
  - scm information

### Publishing Workflow

The new Central Portal has a two-step process:

1. **Deploy**: Upload your artifacts (via `mvn deploy`)
2. **Publish**: Manually publish through the Central Portal UI or API

This is different from OSSRH where the `nexus-staging-maven-plugin` handled both steps.

### Automatic vs Manual Publishing

- By default, deployments require manual publishing via the Central Portal UI
- You can automate publishing using the Central Portal API if needed
- See: https://central.sonatype.com/api-doc for API documentation

## Troubleshooting

### Authentication Failures

If you get authentication errors:
1. Verify your user token is correct in `~/.m2/settings.xml`
2. Ensure the server `<id>` matches: `central`
3. Check that your namespace has been migrated

### Deployment Failures

If deployment fails:
1. Ensure all required artifacts are being generated (sources, javadoc, GPG signatures)
2. Check that your POM contains all required metadata
3. Verify GPG signing is working with your key

### Need Help?

- Central Portal Documentation: https://central.sonatype.org/
- Central Support: Available through the Central Portal
- OSSRH Sunset Documentation: https://central.sonatype.org/pages/ossrh-eol/

## Quick Reference

| Purpose | Old OSSRH | New Central Portal |
|---------|-----------|-------------------|
| Portal URL | oss.sonatype.org | central.sonatype.com |
| Server ID | ossrh | central |
| Deployment | nexus-staging-maven-plugin | maven-deploy-plugin |
| Publishing | Automatic or via plugin | Manual via Portal UI or API |
| Credentials | Username/Password | User Token |

## Next Steps

1. ✅ POM updated (done)
2. ⏳ Update `~/.m2/settings.xml` with your user token
3. ⏳ Generate user token from Central Portal
4. ⏳ Test deployment with: `mvn clean deploy -Pcentral`
5. ⏳ Verify and publish in Central Portal UI

