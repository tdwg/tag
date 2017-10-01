TAG: GUID applicabilty statements

For Comment
@chicoreus @hlapp @baskaufs 
@tucotuco @dhobern @stanblum 

The TDWG Executive has asked that TAG retire, and/or replace, the GUID and LSID [applicability statement](https://github.com/tdwg/tag/issues/9).  But as only they can do that, my understanding is that they are asking TAG to do the work required to retire the standard and/or recommend an LSID strategy.

Though taking down the LSID recommendation is the obvious driver behind this request it is the GUID-AS that is past its use-by date. The LSID-AS is quite okay in that it serves to explain the pattern of LSID usage/examples in our standards and in the literature.  It does not mandate LSID use.

After review of the [GUID AS](http://www.tdwg.org/standards/150) and a lot of external references and commentary, my initial preference was for retirement of the standard, leaving the AS documents, for reference, to be updated and maintained outside of the standards track.  However I now have to agree with Stan ... we *are* going to need a replacement first.  

Retirement of the standards will not  remove the documents.  They are referenced/copied all over the web and their URI will persist - so best that we  continue to deliver something useful from that location.

Fortunately, while there are two statements there is only one applicability standard [(#150)](http://www.tdwg.org/standards/150).  I think this means that it should not be too disruptive to make an interim update of the GUID-AS (to deprecate the LSID preference) and then maintain it at this location with the LSID-AS archived for reference.  As long as we also update all the pages that mention LSID no incoming, external links will be broken.  Though there are many pages/testimonials etc with explicitly references to TDWG+GUID+LSID that are well beyond the reach of TDWG. 

It would be good if TDWG  announce these changes and not just try to slide LSID quietly out of the picture. 

It might also be useful to argue time served, and make a case to wave the usual standards review and ratification process on the interim revision?  

LSID aside, the GUID-AS is past its use-by date and overdue for an overhaul that *will* require adherence to the process standards and a Task Group to carry it through.

The LSID-AS can continue in service  to explain the pattern of LSID usage/examples in our standards and in the literature.  It clearly states the principles behind persistent identifiers and makes a good case for meta-data profiles. It does not mandate LSID use.

I  suggest that to the executive we recommend as follows:

# LSID Recommendation 
in response [Exec. request #90](https://github.com/tdwg/exec/issues/90)

- That the Executive agree to by pass on the usual 60+ day ratification procedure to allow for an immediate, interim revision of the GUID applicability statement. 
- This interim revision only make changes to deprecate the LSID preference and highlight the advantage of HTTP URI.
- The Executive announce these changes to the membership.
- The TAG continue to coordinate a full, maintenance revision of the applicability statements to reflect TDWG policy and to provide guidance on the choice of identifiers:
   - Reconvene an Identifiers Task Group, perhaps from the authors of [Actionable, long-term stable and semantic web compatible identifiers for access to biological collection objects. Database (2017) Vol. 2017: article ID bax003; doi:10.1093/database/ bax003](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5467547/).
   - Work toward an official HTTP URI/Linked Data policy.
   - Migrate, and update, the metadata profile recommendations currently embodied in the lsid-as.
   - Keep the LSID-AS for reference.
- Update [Getting Started page](http://www.tdwg.org/getting-started/) to remove LSID recommendation.
- TDWG hunt down LSID references to be changed and suggest alternative text to page curators.
   - coordinate with web content review
- In most cases examples, code, illustrations etc. using or depicting LSID will not require changes.
