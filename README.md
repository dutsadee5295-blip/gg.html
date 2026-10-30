
-- เปิด RLS ของตาราง user_roles
ALTER TABLE public.user_roles
ENABLE ROW LEVEL SECURITY;

-- ป้องกันการเข้าถึงโดยผู้ที่ไม่ได้เข้าสู่ระบบ
REVOKE ALL ON TABLE public.user_roles
FROM anon;

-- ป้องกันผู้ใช้ที่เข้าสู่ระบบแก้ไขบทบาทโดยตรง
REVOKE INSERT, UPDATE, DELETE
ON TABLE public.user_roles
FROM authenticated;

-- อนุญาตให้ผู้ใช้ที่เข้าสู่ระบบอ่านบทบาทได้
-- แต่ยังต้องผ่าน RLS Policy
GRANT SELECT
ON TABLE public.user_roles
TO authenticated;
