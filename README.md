import React, { useState } from 'react';

// مكون القسم القابل للطي
const CollapsibleSection = ({ item, level = 0, onSelect }) => {
  const [isOpen, setIsOpen] = useState(false);

  const toggleOpen = () => {
    setIsOpen(!isOpen);
  };

  return (
    <div style={{ marginLeft: `${level * 20}px` }}>
      <div
        onClick={() => {
          toggleOpen();
          onSelect(item);
        }}
        style={{
          padding: '10px',
          cursor: 'pointer',
          backgroundColor: level === 0 ? '#e0e0e0' : 'transparent',
          borderRadius: '4px',
          marginBottom: '5px',
          display: 'flex',
          justifyContent: 'space-between',
          alignItems: 'center',
        }}
      >
        <span>{item.name}</span>
        {item.subItems && (
          <span style={{ transition: 'transform 0.3s' }}>
            {isOpen ? '▼' : '▶'}
          </span>
        )}
      </div>
      {isOpen && item.subItems && (
        <div style={{ display: 'flex', flexDirection: 'column' }}>
          {item.subItems.map((subItem, index) => (
            <CollapsibleSection
              key={index}
              item={subItem}
              level={level + 1}
              onSelect={onSelect}
            />
          ))}
        </div>
      )}
    </div>
  );
};

// مكون الشريط الجانبي
const Sidebar = ({ items, onSelect }) => (
  <nav style={{
    width: '300px',
    backgroundColor: '#f8f8f8',
    padding: '20px',
    borderRight: '1px solid #ddd',
    overflowY: 'auto',
    height: '100vh'
  }}>
    {items.map((item, index) => (
      <CollapsibleSection key={index} item={item} onSelect={onSelect} />
    ))}
  </nav>
);

// المكون الرئيسي
const Dashboard = () => {
  const [selectedItem, setSelectedItem] = useState(null);

  const sidebarItems = [
    {
      name: 'الأطباء',
      subItems: [
        { name: 'إضافة طبيب',
          subItems: [
            { name: 'بيانات شخصية' },
            { name: 'مؤهلات' },
            { name: 'جدول المواعيد' }
          ]
        },
        { name: 'قائمة الأطباء' },
        { name: 'التخصصات' },
        { name: 'تقارير الأطباء' }
      ]
    },
    {
      name: 'المرضى',
      subItems: [
        { name: 'إضافة مريض',
          subItems: [
            { name: 'بيانات شخصية' },
            { name: 'التاريخ الطبي' },
            { name: 'الفحوصات' }
          ]
        },
        { name: 'قائمة المرضى' },
        { name: 'السجلات الطبية' },
        { name: 'المواعيد' }
      ]
    },
    {
      name: 'الأدوية',
      subItems: [
        { name: 'إضافة دواء' },
        { name: 'قائمة الأدوية' },
        { name: 'المخزون' },
        { name: 'الطلبيات' }
      ]
    },
    {
      name: 'التحاليل',
      subItems: [
        { name: 'إضافة تحليل' },
        { name: 'قائمة التحاليل' },
        { name: 'النتائج' },
        { name: 'التقارير' }
      ]
    },
    {
      name: 'الأشعة',
      subItems: [
        { name: 'إضافة فحص أشعة' },
        { name: 'قائمة الفحوصات' },
        { name: 'النتائج' },
        { name: 'التقارير' }
      ]
    },
    {
      name: 'الحجوزات',
      subItems: [
        { name: 'إضافة حجز' },
        { name: 'قائمة الحجوزات' },
        { name: 'جدول المواعيد' },
        { name: 'إحصائيات' }
      ]
    },
    {
      name: 'الكشوفات',
      subItems: [
        { name: 'إضافة كشف' },
        { name: 'قائمة الكشوفات' },
        { name: 'التقارير' }
      ]
    },
    {
      name: 'الوصفات الطبية',
      subItems: [
        { name: 'إضافة وصفة' },
        { name: 'قائمة الوصفات' },
        { name: 'الأدوية الموصوفة' },
        { name: 'التقارير' }
      ]
    },
    {
      name: 'الموظفين',
      subItems: [
        { name: 'إضافة موظف' },
        { name: 'قائمة الموظفين' },
        { name: 'الرواتب' },
        { name: 'الإجازات' }
      ]
    },
    {
      name: 'المصروفات والإيرادات',
      subItems: [
        { name: 'إضافة معاملة' },
        { name: 'التقارير المالية' },
        { name: 'الميزانية' }
      ]
    },
    {
      name: 'العملاء والموردين',
      subItems: [
        { name: 'إضافة عميل/مورد' },
        { name: 'قائمة العملاء' },
        { name: 'قائمة الموردين' },
        { name: 'الحسابات' }
      ]
    },
    {
      name: 'الأصناف والمنتجات',
      subItems: [
        { name: 'إضافة صنف' },
        { name: 'قائمة الأصناف' },
        { name: 'التسعير' },
        { name: 'المخزون' }
      ]
    },
    {
      name: 'المشتريات',
      subItems: [
        { name: 'إضافة طلب شراء' },
        { name: 'قائمة الطلبات' },
        { name: 'الفواتير' },
        { name: 'التقارير' }
      ]
    },
    {
      name: 'المبيعات',
      subItems: [
        { name: 'إضافة عملية بيع' },
        { name: 'قائمة المبيعات' },
        { name: 'الفواتير' },
        { name: 'التقارير' }
      ]
    },
    {
      name: 'المستودعات',
      subItems: [
        { name: 'إضافة مستودع' },
        { name: 'قائمة المستودعات' },
        { name: 'الجرد' },
        { name: 'التحويلات' }
      ]
    }
  ];

  return (
    <div style={{ fontFamily: 'Arial, sans-serif', direction: 'rtl', display: 'flex', flexDirection: 'column', minHeight: '100vh' }}>
      <header style={{
        display: 'flex',
        justifyContent: 'space-between',
        alignItems: 'center',
        padding: '10px 20px',
        backgroundColor: '#3a7bd5',
        color: 'white'
      }}>
        <button style={{ backgroundColor: 'transparent', border: 'none', color: 'white', cursor: 'pointer' }}>تسجيل الخروج</button>
        <span>مرحبًا، admin</span>
        <div>
          <button style={{ backgroundColor: 'transparent', border: 'none', color: 'white', cursor: 'pointer', marginRight: '10px' }}>النسخ الاحتياطي</button>
          <button style={{ backgroundColor: 'transparent', border: 'none', color: 'white', cursor: 'pointer' }}>الإعدادات</button>
        </div>
      </header>
      
      <div style={{ display: 'flex', flex: 1 }}>
        <Sidebar items={sidebarItems} onSelect={setSelectedItem} />
        
        <main style={{ flex: 1, padding: '20px', backgroundColor: '#f0f4f8' }}>
          {selectedItem ? (
            <div>
              <h2>{selectedItem.name}</h2>
              {/* هنا يمكن إضافة المحتوى الخاص بكل قسم */}
            </div>
          ) : (
            <div>
              <h2 style={{ textAlign: 'center', color: '#333', marginBottom: '20px' }}>لوحة التحكم الرئيسية</h2>
              {/* هنا يمكن إضافة محتوى لوحة التحكم الرئيسية */}
            </div>
          )}
        </main>
      </div>
    </div>
  );
};

export default Dashboard;
