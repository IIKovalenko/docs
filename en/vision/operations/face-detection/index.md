# Detecting faces in an image

_Face detection is currently at the [Preview stage](/docs/overview/concepts/launch-stages)._

To detect faces in a photo, use the [Face Detection](../../concepts/face-detection/index.md) feature.

In the [batchAnalyze](../../api-ref/Vision/batchAnalyze.md) method, set the `type` property to `FACE_DETECTION`.

## Examples {#examples}

[!INCLUDE [ai-before-beginning](../../../_includes/ai-before-beginning.md)]

### Detecting faces {#basic}

1. Prepare an image file that meets the requirements:

    [!INCLUDE [file-restrictions](../../../_includes/vision/file-restrictions.md)]

    > [!NOTE]
    >
    > Need an image? [Download a sample](https://storage.yandexcloud.net/vision/face-detection-sample.jpg).

1. Encode the file as Base64:

    [!INCLUDE [base64-encode-command](../../../_includes/vision/base64-encode-command.md)]

1. Create a file with the request body (for example, `body.json`). In the `content` property, specify a [Base64-encoded](../base64-encode.md) image:

    **body.json:**

    ```json
    {
        "folderId": "ajk55f3mblj12eghq2oe",
        "analyze_specs": [{
            "content": "iVBORw0KGgo...",
            "features": [{
                "type": "FACE_DETECTION"
            }]
        }]
    }
    ```

1. [!INCLUDE [send-request](../../../_includes/vision/send-request.md)]

### Ready-to-use function for sending requests in bash {#oneliner}

1. [!INCLUDE [cli-install](../../../_includes/cli-install.md)]

1. Copy the function to the terminal:

    ```bash
    vision_face_detection() {
        curl -H "Authorization: Bearer `yc iam create-token`" \
        "https://vision.api.cloud.yandex.net/vision/v1/batchAnalyze" \
        -d @<(cat << EOF
    {
        "folderId": "`yc config get folder-id`",
        "analyze_specs": [{
            "content": "`base64 -i $1`",
            "features": [{
                "type": "FACE_DETECTION"
            }]
        }]
    }
    EOF
    )
    }
    ```

    [!INCLUDE [oneline-function-hints](../../../_includes/vision/oneline-function-hints.md)]

1. Now you can call this function by passing the image path in the arguments:

    ```bash
    vision_face_detection path/to/image.jpg
    ```

