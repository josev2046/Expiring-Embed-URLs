# Vimeo Expiring Embed URLs: Technical Notes

These notes outline the Beta method for generating time-limited embed URLs for Vimeo videos via their API. Note that this functionality requires a Vimeo enterprise account with the relevant capability enabled.

## Generating an Expiring Embed URL

To initiate the generation of an expiring embed URL, a POST request must be directed to one of the following API endpoints:

`POST https://api.vimeo.com/users/{user_id}/videos/{video_id}/expiring_url`

`POST https://api.vimeo.com/me/videos/{video_id}/expiring_url`

`POST https://api.vimeo.com/videos/{video_id}/expiring_url`

`POST https://api.vimeo.com/me/videos/{video_id}/expiring_url`



Successful operation requires the inclusion of the following path parameters:

* `user_id`: The identifier of the Vimeo user account owning the video resource.
* `video_id`: The identifier of the specific video resource for which an expiring embed URL is required.

Furthermore, the following query parameter is mandatory to define the temporal validity of the generated URL:

* `expire_in`: This parameter specifies the duration, in seconds, for which the URL will remain valid.

## Example Request (cURL)

The following illustrates a cURL command to generate an expiring embed URL:

![image](https://github.com/user-attachments/assets/39574ae9-83a3-4743-b403-021b625823b2)


~~~```bash
curl -X POST \
-H "Authorization: Bearer {TOKEN}" \
 -H "Content-Type: application/json" \
 -d '{
  "expire_in": {SECONDS}
 }' \
 "[https://api.vimeo.com/users/](https://api.vimeo.com/users/){USER_ID}/videos/{VIDEO_ID}/expiring_url?expire_in={SECONDS}"
~~~

Upon successful execution, this command will return a Vimeo video link (and associated embed code) with a limited lifespan corresponding to the specified number of seconds. Failure to adhere to the parameter requirements will result in an error response.

HTTP Status Codes and Explanations:

`200 OK`: The expiring embed URL was successfully generated.

`400 Bad Request`: The request was malformed. 

Specific error codes include:

`Error code 2444`: The expire_in parameter was either absent or its value was not greater than one.

`Error code 2445`: The value provided for the expire_in parameter exceeds 86400 seconds (one day).

## DeepWiki Link

https://deepwiki.com/josev2046/Vimeo-Expiring-Embed-URLs
