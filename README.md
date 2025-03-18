// /api/send-verification-email.js
import resend from './resend'; // import the Resend setup

export default async function handler(req, res) {
    if (req.method === 'POST') {
        const { email } = req.body;

        try {
            // Send verification code using Resend API
            await resend.sendEmail({
                to: email,
                subject: 'Verification Code',
                text: 'Your verification code is: 123456', // you can generate a random code
            });

            return res.status(200).json({ success: true });
        } catch (error) {
            console.error('Error sending email:', error);
            return res.status(500).json({ success: false, message: 'Failed to send email' });
        }
    }
}
