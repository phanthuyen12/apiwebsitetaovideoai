# Hướng dẫn sử dụng Shortt Media API trong n8n

Đây là hướng dẫn cách sử dụng **API upload video** `https://media.shortt.top/media/files` trực tiếp trong n8n.

---

## A (chuẩn bị)

- **API Token**: bạn cần token hợp lệ (`Bearer TOKEN`) từ Shortt Media.
- **File video**: `.mp4` hoặc các định dạng được hỗ trợ.

---

## 1. Sử dụng n8n để uploads file 

Trong n8n, bạn có thể dùng node **HTTP Request** hoặc **Execute Python** để upload video:

### A. Dùng node HTTP Request

1. Chọn **HTTP Request** node.
2. Thiết lập:
   - Method: `POST`
   - URL: `https://media.shortt.top/media/files`
   - Authentication: **Header** `Authorization: Bearer YOUR_API_TOKEN`
   - Body Content Type: `Form-Data`
   - Thêm field:
     - Key: `files`
     - Type: `File`
     - Value: chọn file `.mp4` từ local hoặc binary từ node trước
3. Kết quả trả về sẽ là JSON chứa thông tin file đã upload, ví dụ:  
   ```json
   {
     "file_url": "https://media.shortt.top/files/abc123.mp4"
   }
## 2. Tạo Task 

1. Thêm node **HTTP Request**.
2. Cấu hình:
   - **Method**: POST
   - **URL**: `https://b.shortspin.ai/api/video-v2/create`
   - **Authentication**: None (dùng header custom)
   - **Headers**:
     - `Authorization: Bearer YOUR_API_TOKEN`
     - `Content-Type: application/json`
     - `Accept: application/json`
   - **Body Content Type**: Raw JSON
   - **Body**: dán nội dung JSON cấu hình video, ví dụ:

```json
{
 'task_type': 'sp_txt2video_02',
    'input': {
        'prompt': 'Lệnh thắng không chứng minh bạn giỏi.\nTôi từng hãnh diện khi có vài lệnh thắng liên tiếp, nghĩ rằng mình đã giỏi hơn người khác, nhưng rồi chỉ cần một lệnh thua sai lúc, tất cả lợi nhuận quay về con số không, thậm chí âm, điều đó dạy tôi rằng, một lệnh thắng chỉ là kết quả tức thời, bạn cần hàng trăm lệnh đúng nguyên tắc mới chứng minh được thực lực, đừng vội tự hào vì vài kết quả ngắn hạn, sự ổn định mới là điều khó đạt và đáng theo đuổi.',
        'background_music': 'None',
        'voice_name': 'Nam_PhanTich_01',
        'voice_locale': 'vi-VN',
        'size': '768x1344',
        'is_subtitle': True,
        'style': '',
        'font': {
            'name': 'Anton',
            'size': 48,
        },
        'videos': [
            'https://upload.shortspin.ai/2025/11/05/a4a59473-c0ac-472c-b59a-20bbb068ba3a.mp4',
        ],
        'images': [],
        'media': [],
        'text_color': [
            '#282828',
            '#ffffff',
        ],
        'voice_speed': 1,
        'subtitle_theme': 'default',
        'subtitle_position': [
            'center',
            'middle',
        ],
        'uppercase_subs': True,
        'show_end_punctuation': True,
        'max_words_per_line': 4,
        'subtitle_url': '',
        'voice_url': '',
        'background_volume': -20,
        'anim_effect': 'random',
        'hook_name': '',
        'caption': {
            'main': {
                'color': '#00FFFF',
                'font': {
                    'name': 'Anton',
                },
            },
            'sub': {
                'color': '#FFFFFF',
                'font': {
                    'name': 'Anton',
                },
            },
        },
    },
}


