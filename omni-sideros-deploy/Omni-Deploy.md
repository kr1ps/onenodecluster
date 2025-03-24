# Omni Self-Hosted Setup

## Omni Version Checkers
You can check the tagged versions of Omni at the following link:  
[Omni Container Versions](https://github.com/siderolabs/omni/pkgs/container/omni/versions?filters%5Bversion_type%5D=tagged)

## Implementation Notes
This Docker Compose setup is based on a combination of the following documentation:  
- [Omni Self-Hosted Guide (Index-1)](https://omni.siderolabs.com/how-to-guides/self_hosted/index-1)  
- [Omni Self-Hosted Guide (Index)](https://omni.siderolabs.com/how-to-guides/self_hosted/index)  
- Important notes:
  - you need to generate a multidomain cert or wildcard for the three domains if you will use it behind reverse proxy.
  - install sidero-tools https://omni.siderolabs.com/how-to-guides/install-and-configure-omnictl


## SAML Authentication with Authentik
The SAML authentication configuration is based on this [Authentik issue](https://github.com/goauthentik/authentik/issues/9086).

### Docker Container Omni Arguments for SAML
Configure Omni to use SAML authentication by adding the following arguments:

```
--auth-saml-enabled=true
--auth-saml-url=https://<your_authentik_domain>/application/saml/<slug>/metadata/
```

### Authentik Configuration
#### Customization → Property Mappings → Create → SAML Provider Property Mapping
Create a custom property mapping in Authentik:

```
Name: Omni mapping
SAML Attribute Name: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name
Expression: return request.user.email
```

#### Provider Settings (Overrides)
Update the service provider settings with the following values:

```
ACS URL = https://<your_omni_domain>/saml/acs
Service Provider Binding = Post
Audience = https://<your_omni_domain>/saml/metadata
```

#### Advanced Protocol Settings
Modify the advanced protocol settings to include:

```
Signing Certificate: Authentik's self-signed certificate (should be replaceable, but not tested)
Sign Assertions: true
Sign Responses: true
Property Mappings: Omni mapping
NameID Property Mapping: Omni mapping
```

---

This documentation provides a structured setup for integrating Omni with SAML authentication using Authentik.