# XML External Entity (XXE) Injection

XML External Entity (XXE) injection is a vulnerability that allows attackers to interfere with an application's XML processing. By injecting malicious XML entities, attackers can read files on the server, perform SSRF, or cause denial of service.

The existing XXE.md page provides a general overview. This directory contains individual lab writeups.

## Contents

- [Exploiting XXE using external entities to retrieve files](./Exploiting_XXE_using_external_entities_to_retrieve_files.md)
- [Exploiting XXE to perform SSRF attacks](./Exploiting_XXE_to_perform_SSRF_attacks.md)
- [Blind XXE with out-of-band interaction](./Blind_XXE_with_out-of-band_interaction.md)
- [Blind XXE with out-of-band interaction via XML parameter entities](./Blind_XXE_with_out-of-band_interaction_via_XML_parameter_entities.md)
- [Exploiting blind XXE to exfiltrate data using a malicious external DTD](./Exploiting_blind_XXE_to_exfiltrate_data_using_a_malicious_external_DTD.md)
- [Exploiting blind XXE to retrieve data via error messages](./Exploiting_blind_XXE_to_retrieve_data_via_error_messages.md)
- [Exploiting XInclude to retrieve files](./Exploiting_XInclude_to_retrieve_files.md)
- [Exploiting XXE via image file upload](./Exploiting_XXE_via_image_file_upload.md)
- [Exploiting XXE to retrieve data by repurposing a local DTD](./Exploiting_XXE_to_retrieve_data_by_repurposing_a_local_DTD.md)
